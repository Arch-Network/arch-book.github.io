# `getAccountAddress`

**Description:**  Fetches the account address associated with a public key.

**Method:** `POST`

**Parameters:**
    `pubkey: <byte_array>` - The public key ([Pubkey]) of the account.

**Returns:** The account address as a string.

**Request:**
```bash
curl -vL POST -H 'Content-Type: application/json' -d '
{
    "jsonrpc":"2.0",
    "id":1,
    "method":"get_account_address",
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
  "result": "bc1qar0srrr7xfkvy5l643lydnw9re59gtzzwf5mdq",
  "id": "1"
}
```

[Pubkey]: ../../program/pubkey.md

