# `startDkg`

**Description:** Initiates the Distributed Key Generation (DKG) process.

**Method:** `POST`

**Parameters:**
    None.

**Returns:** A success message if the DKG process is initiated.

**Request:**
```bash
curl -vL POST -H 'Content-Type: application/json' -d '
{
    "jsonrpc":"2.0",
    "id":1,
    "method":"start_dkg",
    "params":[]
}' \
http://localhost:9001/
```

**Response:**
```json
{
  "jsonrpc": "2.0",
  "result": "DKG process initiated",
  "id": "1"
}
```

