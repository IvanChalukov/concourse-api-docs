# Well known

### Get OpenID Connect configuration
<details open>
 <summary><code>GET</code> <code><b>/.well-known/openid-configuration</b></code> <code>(retrieves the OpenID Connect configuration)</code></summary>

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | `application/json` | See JSON example below |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "issuer": "http://localhost:8080",
  "jwks_uri": "http://localhost:8080/.well-known/jwks.json",
  "claims_supported": [
    "aud",
    "iat",
    "iss",
    "sub"
  ],
  "response_types_supported": [
    "idtoken"
  ],
  "id_token_signing_alg_values_supported": [
    "RS256",
    "ES256"
  ],
  "subject_types_supported": [
    "public"
  ]
}
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/.well-known/openid-configuration
```
</details>

---

### Get JSON Web Key Set
<details open>
 <summary><code>GET</code> <code><b>/.well-known/jwks.json</b></code> <code>(retrieves the JSON Web Key Set)</code></summary>

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | `application/json` | See JSON example below |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "keys": [
    {
      "use": "sig",
      "kty": "RSA",
      "kid": "7418888054160775771",
      "alg": "RS256",
      "n": "0MqLsB...xJev8",
      "e": "AQAB"
    },
    {
      "use": "sig",
      "kty": "EC",
      "kid": "7516800182609211697",
      "crv": "P-256",
      "alg": "ES256",
      "x": "x5oTbCIVUvr6Ru8HgWqD1SR30TeWq9ZzxTrROgb7khk",
      "y": "O1jtctb1um1QWczezpG1W_6S2r_U8OjF4m9rld911_Y"
    }
  ]
}
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/.well-known/jwks.json
```
</details>

---