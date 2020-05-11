JWT
**session less**
x-access-token: [header].[payload].[signature]

flow:
1. send **Login Data**
2. create **JWT** with 'secret'
3. return **JWT**
4. send Authenticated request with **JWT** in Header
5. validate **JWT**
6. return **Response**

three parts of JWT:
* Header
* Payload
* Signature

header example 
```json
{
    "typ": "JWT",
    "alg": "JS256"      // hash algorithm for generating Token signature
}
```

payload example
```json
{
    "userId": "abcds123456...",
    "username":"somename",
    "email": "someemail@haha.com",
    "iss": "zKoder, author of some.com",  // Issuer: who issued the JWT
    "iat": "1570238918",  // Issued at time the JWT was issued at
    "exp": "1570238992",  // Expiration time: JWT expiration time
}
```

signature
```js
const data = Base64UrlEncode(header) + '.' + Base64UrlEncode(payload);
const hashedData = Hash(data, secret);
const signature = Based64UrlEncode(hashedData)
```

combined
```js
const encodedHeader = base64urlEncode(header);
const encodedPayload = base64urlEncode(payload);
const data = encodedHeader + "." + encodedPayload;
const hashedData = Hash(data, secret);
const HWT = encodedHeader + "." + encodedPayload + "." + sugnature;
```

