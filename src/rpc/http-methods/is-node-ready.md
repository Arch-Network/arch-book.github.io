# `isNodeReady`

**Description:** Checks if the node is ready to process requests.

**Parameters:**
    None.

**Returns:** A boolean indicating whether the node is ready.

**Request:**
```bash
curl -vL POST -H 'Content-Type: application/json' -d '
{
    "jsonrpc":"2.0",
    "id":1,
    "method":"is_node_ready",
    "params":[]
}' \
http://localhost:9001/
```

**Response:**
```json
{
  "jsonrpc": "2.0",
  "result": true,
  "id": "1"
}
```
