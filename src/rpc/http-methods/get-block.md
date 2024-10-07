# `getBlock`

**Description:**  Retrieves block data based on a block hash.

**Method:** `POST`

**Parameters:**
    `blockHash: <string>` - A string representing the block hash.

**Returns:** A `Block` object or `undefined` if the block is not found.

**Error Handling:** Returns `undefined` if the block is not found (404).

**Request:**
```bash
curl -vL POST -H 'Content-Type: application/json' -d '
{
    "jsonrpc":"2.0",
    "id":1,
    "method":"get_block",
    "params":[
        "000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f" 
    ]
}' \
http://localhost:9001/
```

**Response:**
```json
{
  "jsonrpc": "2.0",
  "result": {
    /* Block object */
  },
  "id": "1"
}
```

