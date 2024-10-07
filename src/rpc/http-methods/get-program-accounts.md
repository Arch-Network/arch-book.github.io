# `getProgramAccounts`

Fetches all accounts owned by the specified program ID.

**Parameters:** `program_id: <byte_array>` - Pubkey of the program to query, as an array of 32 bytes.

`filters` (optional) - Array of filter objects, each filter should be either:    
- `{ "DataSize": <size> }` where `<size>` is the required size of the account data
- `{ "DataContent": { "offset": <offset>, "bytes": <byte_array> } }` where `<offset>` is the offset into the account data, and `<byte_array>` is an array of bytes to match

**Returns:** An array of account objects, each containing:
- `pubkey: <byte_array>`: The account's public key.
- `account: <object>`: An object containing the account's data and metadata.

**Request:**
```bash
curl -vL POST -H 'Content-Type: application/json' -d '
{
  "jsonrpc":"2.0",
  "id":1,
  "method": "get_program_accounts",
  "params": [
    [80,82,242,228,43,246,248,133,88,238,139,124,88,96,107,32,71,40,52,251,90,42,66,176,66,32,147,203,137,211,253,40],
    [
      {
        "DataSize": 165
      },
      {
        "DataContent": {
          "offset": 0,
          "bytes": [1, 2, 3, 4]
        }
      }
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
    {
      "pubkey": [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32],
      "account": {
        "data": [1,2,3,4,...],
        "owner": [80,82,242,228,43,246,248,133,88,238,139,124,88,96,107,32,71,40,52,251,90,42,66,176,66,32,147,203,137,211,253,40],
        "utxo": "txid:vout",
        "is_executable": false
      }
    }
  ],
  "id": "1"
}
```
