# `resetNetwork`

**Description:** Resets the network state.

**Parameters:**
    None.

**Returns:** A success message if the network reset is successful.

**Request:**
```bash
curl -vL POST -H 'Content-Type: application/json' -d '
{
  "jsonrpc":"2.0",
  "id":1,
  "method":"reset_network",
  "params":[]
}' \
http://localhost:9001/
```

**Response:**
```json
{
  "jsonrpc": "2.0",
  "result": "Success!",
  "id": "1"
}
```

