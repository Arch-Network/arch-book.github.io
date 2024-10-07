# HTTP Methods

Interact with Arch nodes directly with the JSON RPC API via this list of available HTTP methods.

> INFO:
>
> For client-side needs, use the [@saturnbtcio/arch-sdk] library as an interface for the RPC methods to interact with an Arch node.

### Endpoint
Default port: `9001`
- http://localhost:9001

### Request Format:
To make a JSON-RPC request, send an HTTP `POST` request with a `Content-Type: application/json` header. 

The JSON request data should contain 4 fields:
- `jsonrpc: <string>` - set to "2.0."
- `id: <number>` - a unique client-generated identifying integer.
- `method: <string>` - a string containing the method to be invoked.
- `params: <array>` - a JSON array of ordered parameter values.

### Response Format:
The response output will be a JSON object with the following fields:
- `jsonrpc: <string>` - matching the value set in the request.
- `id: <number>` - matching the value set in the request.
- `result: <array|boolean|number|object|string>` - requested data, success confirmation or boolean flag.


[@saturnbtcio/arch-sdk]: https://www.npmjs.com/package/@saturnbtcio/arch-sdk

