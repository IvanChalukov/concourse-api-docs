# Wall

### Get wall message
<details open>
 <summary><code>GET</code> <code><b>/api/v1/wall</b></code> <code>(retrieves the wall message)</code></summary>

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | `application/json` | See JSON example below |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "message": "This is a wall message",
  "TTL": 3599999994846247400
}
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/wall
```
</details>

---

### Set wall message
<details open>
 <summary><code>PUT</code> <code><b>/api/v1/wall</b></code> <code>(Create/Update the wall message.)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |
> | Content-Type   |  required | string                  | Must be set to `application/json`                                     |

##### Body

> | name      |  type     | data type | description                                      |
> |-----------|-----------|-----------|--------------------------------------------------|
> | message   |  required | string    | The wall message to be displayed                 |
> | ttl       |  optional | integer   | Time to live for the wall message in Nanoseconds. If `ttl` is not provided, message does not expire |

<details>
<summary>Example body</summary>

```json
{
    "message": "This is a wall message.",
    "ttl": 3600
}
```
</details>


##### Responses

| HTTP Code | Content-Type              | Response Example             |
|:---------:|:-------------------------:|:----------------------------:|
| `200`     | None                      | None                         |
| `400`     | text/plain; charset=utf-8 | Wall message cannot be empty |
| `401`     | text/plain; charset=utf-8 | not authorized               |
| `500`     | None                      | None                         |


##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/wall \
  --header 'authorization: Bearer <access_token>' \
  --header 'content-type: application/json' \
  --data '{
  "message": "This is a wall message2",
  "ttl": 3600000000000000000
}'
```
</details>

---

### Clear wall message
<details open>
 <summary><code>DELETE</code> <code><b>/api/v1/wall</b></code> <code>(Clears the wall message.)</code></summary>

##### Headers
> | name           | type     | data type | description                              |
> |----------------|----------|-----------|------------------------------------------|
> | Authorization  | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type | Response Example |
|:---------:|:------------:|:----------------:|
| `200`     | None         | None             |
| `401`     | None         | not authorized   |


##### Example cURL
```shell
curl --request DELETE \
  --url http://localhost:8080/api/v1/wall \
  --header 'authorization: Bearer <access_token>'
```
</details>

---
