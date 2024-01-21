# Fetching Data


## API layer

APIs are an intermediary layer between application code and database.\
There are a few cases where you might use an API:
* If you're using 3rd party services that provide an API.
* If you're fetching data from the client
  - _you want to have an API layer that runs on the server to avoid exposing your database secrets to the client_

In Next.js, you can create API endpoints using [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers).
_They allow you to create custom request handlers for a given route using the Web [Request](https://developer.mozilla.org/ru/docs/Web/API/Request) and [Response](https://developer.mozilla.org/ru/docs/Web/API/Response) APIs._

> **Good to know:** Route Handlers are only available inside the <kbd>app</kbd> directory.
> They are the equivalent of API Routes inside the <kbd>pages</kbd> directory meaning you do not need to use API Routes and Route Handlers together.


## Database queries

When you're creating a full-stack application, you'll also need to write logic to interact with your database. 
For relational databases like Postgres, you can do this with SQL, or an ORM like [Prisma](https://www.prisma.io/).\
There are a few cases where you have to write database queries:
* When creating your API endpoints, you need to write logic to interact with your database.
* If you are using React Server Components (fetching data on the server),
  - _you can skip the API layer, and query your database directly without risking exposing your database secrets to the client._

> By default, Next.js applications use React Server Components.










