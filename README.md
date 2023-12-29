# Next.js synopsis

## 📚 Automatic Installation
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
    - _Production environment variables_
+ 📄 **.env.development**
    - _Development environment variables_
+ 📄 **instrumentation.ts**
    - _OpenTelemetry and Instrumentation file_
+ 📄 **middleware.ts**
    - _Next.js request middleware_

### 💢 Top-level folders 💢
+ 📁 **src** 📁
    - _optional application source folder_
+ 📁 **public** 📁
    - _static assets to be served_
+ 📁 **app** 📁
    - _App Router_

### 💢 App Routing Conventions 💢
+ 📄 **layout.tsx** 📄 Layout
    - _UI that is shared between routes_
    - _should accept and use a `children` prop_
    - _it is not re-rendered during navigation_
+ 📄 **page.tsx** 📄 Page
    - _UI that is unique to a route_
    - _props_
      * `params` - object {dynamic route parameters down to that page}
      * `searchParams` - object {search parameters of the current URL}
+ 📄 **loading.tsx** 📄 Loading UI
    - _create instant loading states built on [Suspense](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming)_
    - `<Suspense key={query + currentPage} fallback={<Skeleton />}>`
+ 📄 **not-found.tsx** 📄 Not found UI
    - _used to render UI when the `notFound` function is thrown within a route segment_
+ 📄 **error.tsx** 📄 Error UI
    - _defines an error UI boundary for a route segment_
    - _useful for catching unexpected errors that occur in Server or Client Components_
    - _props_
      * `error` - instance {Error} forwarded to Client Component
      * `error.message`
      * `error.digest` - automatically generated hash thrown in a Server Component
      * `reset` - function will try to re-render the Error boundary's contents
+ 📄 **global-error.tsx** 📄 Global error UI
    - _to specifically handle errors in root layout_ 
+ 📄 **route.ts** 📄 API endpoint
    - _allows you to create custom request handlers for a given route_
    - _Route Handlers are only available inside the app directory_
    - _params_
      * `request` - {NextRequest} an extension of the Web Request API
      * `context` - {dynamic route parameters for the current route}    
+ 📄 **template.tsx** 📄 Re-rendered layout
    - _create a new instance for each children on navigation_

### 💢 Nested Routes 💢
+ 📁 **/folderA** 📁 Route segment
+ 📁 **/folderA/folderB** 📁 Nested route segment

### 💢 Dynamic Routes 💢
+ 📁 **[folderX]** 📁 Dynamic route segment
    - for example, [id] or [slug]
    - are passed as params prop to layout, page, route, and generateMetadata functions
+ 📁 **[...folderY]** 📁 Catch-all route segment
+ 📁 **[[...folderW]]** 📁 Optional catch-all route segment

### 💢 Route Groups and Private Folders 💢
+ 📁 **(folderX)** 📁 Group routes without affecting routing
    - organize routes without affecting the URL
    - create a group to keep related routes together
    - share the same layout into the group
+ 📁 **_folderX** 📁 Opt folder and all child segments out of routing
    - to create private folders
    - separating UI logic from routing logic

### 💢 Parallel and Intercepted Routes 💢
+ 📁 **@folder** 📁 Named slot
+ 📁 **(.)folder** 📁 Intercept same level
+ 📁 **(..)folder** 📁 Intercept one level above
+ 📁 **(..)(..)folder** 📁 Intercept two levels above
+ 📁 **(...)folder** 📁 Intercept from root

## 📚 Metadata File Conventions

### 💢 App Icons 💢
+ 📄 **favicon.ico** 📄 Favicon file
    - Add this image file to the root `/app` route segment.
    - ``<link rel="icon" href="/favicon.ico" sizes="any" />``
+ 📄 **icon.(ico|jpg|jpeg|png|svg)** 📄 App Icon file
    - ``<link rel="icon" href="/icon?<generated> type="image/<generated>" />"``
+ 📄 **apple-icon.(jpg|jpeg|png)** 📄
    - ``<link rel="apple-touch-icon" href="/apple-icon?<generated>" type="image/<generated>" />``
+ 📄 **icon.tsx** 📄 Generated App Icon


### 💢 SEO 💢
+ 📄 **sitemap.xml** 📄 Sitemap file
    - special file that matches the Sitemaps XML format
    - to help search engine crawlers index your site more efficiently
    - place it in the root of your app directory
+ 📄 **sitemap.ts** 📄 Generated Sitemap
    - to programmatically generate a sitemap by exporting a default function
+ 📄 **robots.txt** 📄 Robots file
    - file that matches the Robots Exclusion Standard
    - to tell search engine crawlers which URLs they can access on your site
+ 📄 **robots.ts** 📄 Generated Robots file
    - file that returns a Robots object

### 💢 Open Graph and Twitter Images 💢













