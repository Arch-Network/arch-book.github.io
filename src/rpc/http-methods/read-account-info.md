# `readAccountInfo`

**Description:**  Retrieves detailed information for the specified account.

**Method:** `POST`

**Parameters:**
    `pubkey: <byte_array>` - The public key ([Pubkey]) of the account to query, as an array of 32 bytes.

**Returns:** An object containing the account's information:
- `data`: The account's data as a byte array.
- `owner`: The account's owner as a byte array (`program_id`).
- `utxo`: The UTXO associated with this account.
- `is_executable`: A boolean indicating if the account contains executable code.

**Request:**
```bash
curl -vL POST -H 'Content-Type: application/json' -d '
{
    "jsonrpc":"2.0",
    "id":1,
    "method":"read_account_info",
    "params":[
        [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32]
    ]
}' \
http://localhost:9001/
```

**Response:**
```json
{
  "jsonrpc": "2.0",
  "result": {
    "data": [1,2,3,4,...],
    "owner": [80,82,242,228,43,246,248,133,88,238,139,124,88,96,107,32,71,40,52,251,90,42,66,176,66,32,147,203,137,211,253,40],
    "utxo": "txid:vout",
    "is_executable": false
  },
  "id": "1"
}
```

[Pubkey]: ../../program/pubkey.md

