# `getBlockHash`

**Description:**  Retrieves the block hash at a specific block height.

**Method:** `POST`

**Parameters:**
    `blockHeight: <number>` - The block height for which to retrieve the block hash.

**Returns:** A string representing the block hash.

**Request:**
```bash
curl -vL POST -H 'Content-Type: application/json' -d '
{
    "jsonrpc":"2.0",
    "id":1,
    "method":"get_block_hash",
    "params":["680000"]
}' \
http://localhost:9001/
```

**Response:**
```json
{
  "jsonrpc": "2.0",
  "result": "000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f",
  "id": "1"
}
```

