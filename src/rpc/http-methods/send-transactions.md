# `sendTransactions`

**Description:**  Sends multiple transactions in a single batch request.

The following pre-flight checks are performed:
1. It verifies the transaction size limit.
2. It verifies the transaction signatures.
3. It verifies that the UTXOs are not already spent.

_The same checks are performed on [sendTransaction]._

If these checks pass, the transaction is forwarded to the rest of the nodes for processing.

**Method:** `POST`

**Parameters:**
    `params: <array[serialized_object]>` - An array of serialized [Runtime Transaction] objects to be sent.

**Returns:** An array of strings containing the transaction IDs (`txids`) of the submitted transactions.

**Request:**
```bash
curl -vL POST -H 'Content-Type: application/json' -d '
{
    "jsonrpc":"2.0",
    "id":1,
    "method":"send_transactions",
    "params": [
        [
            [1,2,3,4,...],
            [5,6,7,8,...]
        ]
    ]
}' \
http://localhost:9001/
```

**Response:**
```json
{
  "jsonrpc": "2.0",
  "result": [
    "1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
    "abcdef1234567890abcdef1234567890abcdef1234567890abcdef1234567890"
  ],
  "id": "1"
}
```

[Runtime Transaction]: ../../sdk/runtime-transaction.md

