# Next.js synopsis

## Automatic Installation
To create a project, run: ``npx create-next-app@latest``.
>   + What is your project named? => my-app-name
>   +  Would you like to use TypeScript? => Yes
>   +  Would you like to use ESLint? => Yes
>   +  Would you like to use Tailwind CSS? => No
>   +  Would you like to use `src/` directory? => Yes
>   +  Would you like to use App Router? (recommended) => Yes
>   +  Would you like to customize the default import alias (@/*)? => No

## 📚 Project Structure

### 💢 Top-level files 💢
+ 📄 **package.json**
    - _Project dependencies and scripts_
+ 📄 **next-env.d.ts**
    - _TypeScript declaration file for Next.js_
+ 📄 **next.config.js**
    - _Configuration file for Next.js_
+ 📄 **tsconfig.json**
    - _Configuration file for TypeScript_
+ 📄 **.eslintrc.json**
    - _Configuration file for ESLint_
+ 📄 **.gitignore**
    - _Git files and folders to ignore_
+ 📄 **.env**
    - _Environment variables_
+ 📄 **.env.local**
    - _Local environment variables_
+ 📄 **.env.production**
    - _	Production environment variables_
+ 📄 **.env.development**
    - _Development environment variables_
+ 📄 **instrumentation.ts**
    - _OpenTelemetry and Instrumentation file_
+ 📄 **middleware.ts**
    - _Next.js request middleware_

### 💢 Top-level folders 💢
+ 📁 **src**
    - _application source folder_
+ 📁 **public**
    - _	Static assets to be served_

### 📚 App Routing Conventions
+ 📄 **layout.tsx**
    - _UI that is shared between routes_
    - _should accept and use a `children` prop_
    - _it is not re-rendered during navigation_
+ 📄 **page.tsx**
    - _UI that is unique to a route_
    - _props_
      * `params` - object {dynamic route parameters down to that page}
      * `searchParams` - object {search parameters of the current URL}
+ 📄 **loading.tsx**
    - _create instant loading states built on [Suspense](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming)_
    - `<Suspense key={query + currentPage} fallback={<Skeleton />}>`
+ 📄 **not-found.tsx**
    - _used to render UI when the `notFound` function is thrown within a route segment_
+ 📄 **error.tsx**
    - _defines an error UI boundary for a route segment_
    - _useful for catching unexpected errors that occur in Server or Client Components_
    - _props_
      * `error` - instance {Error} forwarded to Client Component
      * `error.message`
      * `error.digest` - automatically generated hash thrown in a Server Component
      * `reset` - function will try to re-render the Error boundary's contents
+ 📄 **route.ts**
    - _allows you to create custom request handlers for a given route_
    - _Route Handlers are only available inside the app directory_
    - _params_
      * `request` - {NextRequest} an extension of the Web Request API
      * `context` - {dynamic route parameters for the current route}    
+ 📄 **template.tsx**
    - _create a new instance for each children on navigation_

#### Nested Routes
+ 📁 **/folderA**
+ 📁 **/folderA/folderB**

#### Dynamic Routes
+ 📁 **[folderX]**
+ 📁 **[...folderY]**














