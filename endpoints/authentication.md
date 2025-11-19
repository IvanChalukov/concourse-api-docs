# Authentication Endpoints

### Login

<details open>
 <summary><code>POST</code> <code><b>/sky/issuer/token</b></code> <code>(issues a new token)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Basic auth header with client credentials (Base64 encoded)               |
> | Content-Type   |  required | string                  | Must be set to `application/x-www-form-urlencoded`                        |

##### Body Parameters

> | name      |  type     | data type               | description                                                           |
> |-----------|-----------|-------------------------|-----------------------------------------------------------------------|
> | username  |  required | string                  | The username of the user trying to authenticate                       |
> | password  |  required | string                  | The password of the user trying to authenticate                       |
> | grant_type|  required | string                  | Must be set to `password`                                         |
> | scope     |  optional | string                  | The scopes to be included in the issued token (space-separated)          |


##### Responses

| HTTP Code | Content-Type                | Response                                                                                                   |
|-----------|-----------------------------|------------------------------------------------------------------------------------------------------------|
| `200`     | `application/json`          | `{ "access_token": "<access_token>", "token_type": "bearer", "expires_in": <expires_in>, "id_token": "<id_token>" }` |
| `401`     | `application/json`          | `{ "error": "access_denied", "error_description": "Invalid username or password" }`                        |
| `500`     | `text/html;charset=utf-8`   | None                                                                                                       |

##### Example cURL

```shell
curl --request POST \
  --url http://localhost:8080/sky/issuer/token \
  --header 'authorization: Basic Zmx5OlpteDU=' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data username=<username> \
  --data password=<password> \
  --data grant_type=password \
  --data 'scope=openid profile email federated:id groups'
```

</details>

### Logout

<details open>
 <summary><code>GET</code> <code><b>/sky/logout</b></code> <code>(revokes the current token)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token
> | Content-Type   |  required | string                  | Must be set to `application/x-www-form-urlencoded`                        |
> | Cookie         |  required | string                  | Must include the `skymarshal_auth` cookie with the access token                 |

##### Parameters
> None

##### Responses
| HTTP Code  | Content-Type                | Response |
|-----------|-----------------------------|----------|
| `200`     | `application/json`          | ` ` |
| `401`     | `application/json`          | ` ` |
| `500`     | `application/json`   | None     |

##### Example cURL

```shell
curl --request GET \
  --url http://localhost:8080/sky/logout \
  --header 'authorization: Bearer <token>' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --header 'cookie: skymarshal_auth="bearer <access_token>";' \
  --cookie 'skymarshal_auth="bearer <access_token>";'
```