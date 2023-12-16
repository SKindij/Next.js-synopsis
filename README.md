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
+ 📄 **page**
    - __
+ 📄 ****
    - __
+ 📄 ****
    - __
+ 📄 ****
    - __
+ 📄 ****
    - __
+ 📄 ****
    - __
+ 📄 ****
    - __














