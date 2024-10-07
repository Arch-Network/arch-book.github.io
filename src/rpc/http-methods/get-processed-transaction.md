# `getProcessedTransaction`

**Description:**  Fetches details of a processed transaction using a transaction ID.

**Method:** `POST`

**Parameters:**
    `txid: <string>` - A string representing the transaction ID.

**Returns:** A `ProcessedTransaction` object or undefined if the transaction is not found.

**Error Handling:** Returns `undefined` if the transaction is not found (404).

**Request:**
```bash
curl -vL POST -H 'Content-Type: application/json' -d '
{
    "jsonrpc":"2.0",
    "id":1,
    "method":"get_processed_transaction",
    "params":[
        "1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef"
    ]
}' \
http://localhost:9001/
```

**Response:**
```json
{
  "jsonrpc": "2.0",
  "result": {
    "runtime_transaction": { /* RuntimeTransaction object */ },
    "status": "Confirmed",
    "bitcoin_txids": ["txid1", "txid2"]
  },
  "id": "1"
}
```

