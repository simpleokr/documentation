---
layout: page
title: Authentication
parent: Developer API
---

# Authentication

Simple OKR uses API keys to authenticate requests. You can manage API keys via
[Simple OKR website](https://simpleokr.com).

## API Keys

API keys consist of public and secret components.

Public component (called `Credential`) is used to identify the API key on
Simple OKR servers. The secret component (called `Secret Key`) is used to
construct a request signature. The secret component should be kept private and
not shared with anyone.

## S1-HMAC-SHA256 authentication protocol

`S1-HMAC-SHA256` is the first version of authentication protocol used by the
Simple OKR API.

All requests must include HTTP `Authorization` header in the following format:

```
Authorization: S1-HMAC-SHA256 Credential=<credential>&Timestamp=<timestamp>&Signature=<signature>
```

Authorization header arguments:

- **credential** is the public component of the API key.
- **timestamp** is the RFC 3339 timestamp of the current time in UTC. Your clock must be synchronized. We will allow 10 minute clock skew in either direction.
- **signature** is a signature constructed using the secret key, credential and the timestamp.

The signature is constructed by concatenating `credential` with `timestamp` and
applying HMAC-SHA256 with the secret key. The output of HMAC must be encoded in
hex and converted to lower case. This value becomes the signature.

Below are examples API keys and the signature they should produce. Use this example to validate
your own signature generation methods:

- Credential: `mycredential`
- Secret key: `mysecret`
- Timestamp: `2019-02-03T01:55:37Z`
- Signature: `ab9b15c8321dd0e00bbbcc8e33629adcb273b1dfeedb54387cb305fca6c409fa`

Example signature generation with Go:

```go
import (
  "crypto/hmac"
  "crypto/sha256"
  "encoding/hex"
  "strings"
  "time"
)

func hmacSign(secret string, data string) string {
  mac := hmac.New(sha256.New, []byte(secret))
  mac.Write([]byte(data))
  return strings.ToLower(hex.EncodeToString(mac.Sum(nil)))
}

func main() {
  credential := "mycredential"
  secret := "mysecret"
  timestamp := time.Now().UTC().Format(time.RFC3339)

  signature := hmacSign(secret, credential+timestamp)
  println(credential, secret, timestamp, signature)
}

```

Example signature generation with Python 3:

```python
import hmac
import hashlib

credential = b"mycredential"
secret = b"mysecret"
timestamp = b"2019-02-03T01:55:37Z"

mac = hmac.new(bytearray(secret), digestmod=hashlib.sha256)
mac.update(bytearray(credential + timestamp))
digest = mac.hexdigest()

print(credential, secret, timestamp, digest
```
