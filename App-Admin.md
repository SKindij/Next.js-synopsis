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
  };
```

> You can use the pages option to specify the route for custom sign-in, sign-out, and error pages.














