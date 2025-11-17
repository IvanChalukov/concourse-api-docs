# Authentication Endpoints

<!-- <details>
 <summary><code>POST</code> <code><b>/</b></code> <code>(overwrites all in-memory stub and/or proxy-config)</code></summary>

##### Parameters

> | name      |  type     | data type               | description                                                           |
> |-----------|-----------|-------------------------|-----------------------------------------------------------------------|
> | None      |  required | object (JSON or YAML)   | N/A  |


##### Responses

> | http code     | content-type                      | response                                                            |
> |---------------|-----------------------------------|---------------------------------------------------------------------|
> | `201`         | `text/plain;charset=UTF-8`        | `Configuration created successfully`                                |
> | `400`         | `application/json`                | `{"code":"400","message":"Bad Request"}`                            |
> | `405`         | `text/html;charset=utf-8`         | None                                                                |

##### Example cURL

> ```javascript
>  curl -X POST -H "Content-Type: application/json" --data @post.json http://localhost:8889/
> ```

</details>
 -->
### Login

<details>
 <summary><code>POST</code> <code><b>/sky/issuer/token</b></code> <code>(issues a new token)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Basic auth header with client credentials (Base64 encoded)               |
> | Content-Type   |  required | string                  | Must be set to `application/x-www-form-urlencoded`                        |

##### Parameters

> | name      |  type     | data type               | description                                                           |
> |-----------|-----------|-------------------------|-----------------------------------------------------------------------|
> | username  |  required | string                  | The username of the user trying to authenticate                       |
> | password  |  required | string                  | The password of the user trying to authenticate                       |
> | grant_type|  required | string                  | Must be set to `password`                                         |
> | scope     |  optional | string                  | The scopes to be included in the issued token (space-separated)          |


##### Responses

> | http code     | content-type                      | response                                                            |
> |---------------|-----------------------------------|---------------------------------------------------------------------|
> | `201`         | `text/plain;charset=UTF-8`        | `Configuration created successfully`                                |
> | `400`         | `application/json`                | `{"code":"400","message":"Bad Request"}`                            |
> | `405`         | `text/html;charset=utf-8`         | None                                                                |

##### Example cURL

```shell
curl --request POST \
  --url https://concourse.cf.concourse-dev.concourse-azure.sapcloud.io/sky/issuer/token \
  --header 'authorization: Basic Zmx5OlpteDU=' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data username=<username> \
  --data password=<password> \
  --data grant_type=password \
  --data 'scope=openid profile email federated:id groups'
```

</details>

### Logout
<details>
 <summary><code>GET</code> <code><b>/sky/logout</b></code> <code>(revokes the current token)</code></summary>
##### Parameters