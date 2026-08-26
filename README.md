# CORS for Zen

A standalone CORS library for Zen HTTP servers.

CORS provides a simple API for configuring cross-origin access, allowed methods and headers, credentials, exposed headers, and preflight caching.

## Installation

Install the package using the Zen package manager:

    zen install cors

## Import

    import (Cors, create) from "cors"

## Usage

Create a CORS configuration with `create()`:

    import (Cors, create) from "cors"

    Cors cors = create()

    cors.allow("*")
    cors.methods("GET, POST, PUT, DELETE, OPTIONS")
    cors.headers("Content-Type, Authorization")
    cors.expose("X-Request-ID")
    cors.credentials(true)
    cors.maxAge(86400)

Apply the configuration to an incoming request:

    cors.apply(req)

## Complete Example

    import (Cors, create) from "cors"

    Cors cors = create()

    cors.allow("http://localhost:5173")
    cors.methods("GET, POST, PUT, DELETE, OPTIONS")
    cors.headers("Content-Type, Authorization")
    cors.expose("X-Request-ID")
    cors.credentials(true)
    cors.maxAge(86400)

    HttpServer server = httpServer.create(8080)

    if (server.listen() == 1) {
        screen("Server listening on :8080")

        while (true) {
            HttpRequest req = server.next()

            cors.apply(req)

            req.send("Hello from CORS")
        }
    }

## Configuration

### Origin

Allow a specific origin:

    cors.allow("http://localhost:5173")

Allow any origin:

    cors.allow("*")

### Methods

Configure allowed HTTP methods as a single comma-separated string:

    cors.methods("GET, POST, PUT, DELETE, OPTIONS")

### Headers

Configure allowed request headers as a single comma-separated string:

    cors.headers("Content-Type, Authorization")

### Exposed Headers

Configure exposed response headers:

    cors.expose("X-Request-ID")

Multiple headers can be provided as a comma-separated string:

    cors.expose("X-Request-ID, X-Request-Time")

### Credentials

Enable credentials:

    cors.credentials(true)

### Preflight Cache

Set the preflight cache duration in seconds:

    cors.maxAge(86400)

## Preflight Requests

For a request such as:

    OPTIONS /test
    Origin: http://localhost:5173
    Access-Control-Request-Method: POST
    Access-Control-Request-Headers: Content-Type

`cors.apply(req)` handles the CORS preflight response.

Example response:

    HTTP/1.1 204 OK
    Access-Control-Allow-Origin: http://localhost:5173
    Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS
    Access-Control-Allow-Headers: Content-Type, Authorization
    Access-Control-Expose-Headers: X-Request-ID
    Access-Control-Allow-Credentials: true
    Access-Control-Max-Age: 86400

## API

| Function | Description |
|---|---|
| `create()` | Creates a new CORS configuration |
| `cors.allow(origin)` | Sets the allowed origin |
| `cors.methods(methods)` | Sets allowed methods |
| `cors.headers(headers)` | Sets allowed request headers |
| `cors.expose(headers)` | Sets exposed response headers |
| `cors.credentials(bool)` | Enables or disables credentials |
| `cors.maxAge(seconds)` | Sets the preflight cache duration |
| `cors.apply(req)` | Applies CORS handling to an `HttpRequest` |

## Framework Independent

CORS is a standalone library for Zen.

It is not tied to Drift or any other HTTP framework and works directly with Zen's `HttpRequest` API.

## Package Information

- Name: `cors`
- Version: `1.0.0`
- Author: Jishith-dev
- Repository: https://github.com/Jishith-dev/cors
