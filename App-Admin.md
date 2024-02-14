# Next App Admin
&emsp;_Authentication is a key part of many web applications today. It's how a system checks if the user is who they say they are._

## [Authentication vs. Authorization](https://nextjs.org/docs/app/building-your-application/authentication)

+ **Authentication** is about making sure the user is who they say they are.
  - You're proving your identity with something you have like a username and password.
+ **Authorization** is the next step.
  - Once a user's identity is confirmed, authorization decides what parts of the application they are allowed to use.

> So, authentication checks who you are, and authorization determines what you can do or access in the application.

## [NextAuth.js](https://authjs.dev/reference/nextjs)

&emsp;NextAuth.js abstracts away much of the complexity involved in managing sessions, sign-in and sign-out, and other aspects of authentication.
While you can manually implement these features, the process can be time-consuming and error-prone.\
&emsp;NextAuth.js simplifies the process, providing a unified solution for auth in Next.js applications.

1. Setting up NextAuth.js
    + ``npm install next-auth@beta``
2. Generate a secret key for your application.
    + ``openssl rand -base64 32``
    + _is used to encrypt cookies, ensuring the security of user sessions_
3. In your **.env** file, add your generated key to the `AUTH_SECRET` variable:
    + ``AUTH_SECRET=your-secret-key``

&emsp;For auth to work in production, you'll need to update your environment variables in your Vercel project too.
Check out [this guide](https://vercel.com/docs/projects/environment-variables) on how to add environment variables on Vercel.

### Configuration options for NextAuth.js

Create an **auth.config.ts** file at the root of our project that exports an authConfig object.

```typescript
  import type { NextAuthConfig } from 'next-auth';
 
  export const authConfig = {
    pages: {
      signIn: '/auth/login',
    },
    callbacks: {
      authorized({ auth, request: { nextUrl } }) {
        const isLoggedIn = !!auth?.user;
        const isOnDashboard = nextUrl.pathname.startsWith('/dashboard');
        if (isOnDashboard) {
          if (isLoggedIn) return true;
          return false; // Redirect unauthenticated users to login page
        } else if (isLoggedIn) {
          return Response.redirect(new URL('/dashboard', nextUrl));
        }
        return true;
      },
    },
    providers: [], // Add providers with an empty array for now
  } satisfies NextAuthConfig;
```

> &emsp;You can use the pages option to specify the route for custom sign-in, sign-out, and error pages.\
>
> &emsp;The `authorized` callback is used to verify if the request is authorized to access a page via Next.js Middleware.
> It is called before a request is completed. The `auth` property contains the user's session, and the `request` property contains the incoming request.
>
> &emsp;The `providers` option is an array where you list different login options.

In the root of your project, create a file called **middleware.ts** and paste the following code:
```typescript
  import NextAuth from 'next-auth';
  import { authConfig } from './auth.config';
 
  export default NextAuth(authConfig).auth;
 
  export const config = {
    // https://nextjs.org/docs/app/building-your-application/routing/middleware#matcher
    matcher: ['/((?!api|_next/static|_next/image|.*\\.png$).*)'],
  };
```

> &emsp;Here you're initializing NextAuth.js with the `authConfig` object and exporting the `auth` property.
> You're also using the `matcher` option from Middleware to specify that it should run on specific paths.

### Password hashing
&emsp;_It's good practice to hash passwords before storing them in a database. 
Hashing converts a password into a fixed-length string of characters, which appears random, providing a layer of security even if the user's data is exposed._

&emsp;Create a separate **auth.ts** file for the `bcrypt` package. This is because `bcrypt` relies on Node.js APIs not available in Next.js Middleware.
```typescript
  import NextAuth from 'next-auth';
  import { authConfig } from './auth.config';
  import Credentials from 'next-auth/providers/credentials';
  import { z } from 'zod';
  import { sql } from '@vercel/postgres';
  import type { User } from '@/app/lib/definitions';
  import bcrypt from 'bcrypt';

  // function that queries the user from the database
  async function getUser(email: string): Promise<User | undefined> {
    try {
      const user = await sql<User>`SELECT * FROM users WHERE email=${email}`;
      return user.rows[0];
    } catch (error) {
      console.error('Failed to fetch user:', error);
      throw new Error('Failed to fetch user.');
    }
  };

  export const { auth, signIn, signOut } = NextAuth({
    ...authConfig,
    providers: [Credentials({
      // to handle the authentication logic
      async authorize(credentials) {
        // to validate email and password before checking if user exists in database
        const parsedCredentials = z
          .object({ email: z.string().email(), password: z.string().min(6) })
          .safeParse(credentials);

        if (parsedCredentials.success) {
          const { email, password } = parsedCredentials.data;
		      // queries the user from the database
          const user = await getUser(email);
          if (!user) return null;
		      // to check if the passwords match
		      const passwordsMatch = await bcrypt.compare(password, user.password);
		      if (passwordsMatch) return user;
        }
	      console.log('Invalid credentials');
        return null;	
      },
    })],
  });
```

> &emsp;[Credentials](https://authjs.dev/getting-started/providers/credentials-tutorial) allows users to log in with a username and a password.\
> Generally recommended to use alternative providers such as [OAuth](https://authjs.dev/getting-started/providers/oauth-tutorial) or [email](https://authjs.dev/getting-started/providers/email-tutorial) providers.

### Login Form







