# `getBlockCount`

**Description:**  Retrieves the current block count.

**Method:** `POST`

**Parameters:**
    None.

**Returns:** The current block count as a number. 

**Request:**
```bash
curl -vL POST -H 'Content-Type: application/json' -d '
{
    "jsonrpc":"2.0",
    "id":1,
    "method":"get_block_count",
    "params":[]
}' \
http://localhost:9001/
```

**Response:**
```json
{
  "jsonrpc": "2.0",
  "result": 680000,
  "id": "1"
}
```
