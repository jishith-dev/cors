# CORS for Zen

Author: Jishith-dev

A standalone CORS library for Zen HTTP servers.

Provides a simple API for configuring cross-origin access, allowed methods and headers, credentials, exposed headers, and preflight caching.

## Installation

    zen install cors

## Import

    import (Cors) from "cors"

## Usage

    import (Cors) from "cors"

    Cors cors
    cors.setOrigin("*")
    cors.setMethods("GET, POST, PUT, DELETE, OPTIONS")
    cors.setHeaders("Content-Type, Authorization")
    cors.setExposeHeaders("X-Request-ID")
    cors.setCredentials(true)
    cors.setMaxAge(86400)

Apply the configuration to an incoming request:

    cors.apply(req)

## Complete Example

    import (Cors) from "cors"

    Cors cors
    cors.setOrigin("http://localhost:5173")
    cors.setMethods("GET, POST, PUT, DELETE, OPTIONS")
    cors.setHeaders("Content-Type, Authorization")
    cors.setExposeHeaders("X-Request-ID")
    cors.setCredentials(true)
    cors.setMaxAge(86400)

    HttpServer server = httpServer.create(8080)

    if (server.listen() == 1) {
        screen("Server listening on :8080")

        while (true) {
            HttpRequest req = server.next()

            cors.apply(req)

            req.send("Hello from CORS")
        }
    }

## Defaults

`Cors` works out of the box with no setup:

    Cors cors
    cors.apply(req)

Defaults:

- Origin: `*`
- Methods: `GET, POST, PUT, DELETE, OPTIONS`
- Headers: `Content-Type, Authorization`
- Expose headers: none
- Credentials: `false`
- Max age: `86400`

## Configuration

| Method | Description |
|---|---|
| `setOrigin(origin)` | Sets the allowed origin, e.g. `"*"` or `"http://localhost:5173"` |
| `setMethods(methods)` | Sets allowed HTTP methods as a comma-separated string |
| `setHeaders(headers)` | Sets allowed request headers as a comma-separated string |
| `setExposeHeaders(headers)` | Sets exposed response headers |
| `setCredentials(bool)` | Enables or disables credentials |
| `setMaxAge(seconds)` | Sets the preflight cache duration in seconds |
| `apply(req)` | Applies all configured CORS headers to an `HttpRequest` |

`setExposeHeaders` and `setCredentials` only emit their headers when set — an empty expose string or `false` credentials are silently skipped.

## Framework Independent

CORS is a standalone library for Zen. It is not tied to Drift or any other HTTP framework and works directly with Zen's `HttpRequest` API.

## License

MIT

## Package Information

- Name: `cors`
- Version: `1.0.1`
- Author: Jishith-dev
- Repository: https://github.com/Jishith-dev/cors
