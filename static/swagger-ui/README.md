# Swagger UI

This directory contains HTML, Javascript, and CSS assets
that dynamically generate Swagger documentation from a
[OpenAPI Specification Version 2.0](https://swagger.io/docs/specification/2-0/basic-structure/).
That file is auto-generated by running `make proto` in the root
of this repository. The static assets are copied from the
[dist folder](https://github.com/swagger-api/swagger-ui/tree/master/dist).
After copying, [`swagger-initializer.js`](./swagger-initializer.js)
is edited to load the swagger file from the local server instead of the default petstore.

SwaggerUI is licensed under Apache 2.0 license.
