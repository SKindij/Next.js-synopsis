# Fetching Data


## API layer

APIs are an intermediary layer between application code and database.\
There are a few cases where you might use an API:
* If you're using 3rd party services that provide an API.
* If you're fetching data from the client
  - _you want to have an API layer that runs on the server to avoid exposing your database secrets to the client_

In Next.js, you can create API endpoints using [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers).
> _They allow you to create custom request handlers for a given route using the Web [Request](https://developer.mozilla.org/ru/docs/Web/API/Request) and [Response](https://developer.mozilla.org/ru/docs/Web/API/Response) APIs._




