# Teams

### List all teams

<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams</b></code> <code>(retrieves the teams)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | `application/json` | See JSON example below |
> No unauthorized (401) response is returned, but if authorization header is missing returns an empty `[]`.

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "id": 1,
    "name": "main",
    "auth": {
      "owner": {
          "groups": [],
          "users": [
            "oidc:john",
            "local:test"
          ]
      }
    }
  }
]

```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams \
  --header 'authorization: Bearer <access_token>'
```
</details>

---

### Get team details

<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}</b></code> <code>(retrieves the team details)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | `application/json` | See JSON example below |
| `401`     | text/plain; charset=utf-8 | not authorized  |
<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "id": 1,
  "name": "main",
  "auth": {
    "owner": {
      "groups": [],
      "users": [
        "oidc:john",
        "local:test"
      ]
    }
  }
}
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main \
  --header 'authorization: Bearer <access_token>'
```
</details>

---

### Set team configuration

<details open>
 <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}</b></code> <code>(Create a team)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |
> | Content-Type   |  required | string                   | Must be set to `application/json`                                     |

##### Body

> | name      |  type     | data type | description                                      |
> |-----------|-----------|-----------|--------------------------------------------------|
> | auth      | required  | json      | Team configuration |

<details>
<summary>JSON Example for Body</summary>

```json
{
  "auth": {
    "owner": {
      "groups": [],
      "users": [
        "local:test"
      ]
    }
  }
}
```
</details>

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | `application/json` | See JSON example below |
| `201`     | `application/json` | See JSON example below |
| `401`     | text/plain; charset=utf-8 | not authorized  |
| `400`     | None | None |
<details>
<summary>JSON Example for 200/201 Response</summary>

```json
{
  "team": {
    "id": 3,
    "name": "team",
    "auth": {
      "owner": {
        "groups": [],
        "users": [
          "local:test"
        ]
      }
    }
  }
}
```
</details>

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/team \
  --header 'authorization: Bearer <access_token>' \
  --header 'content-type: application/json' \
  --data '{
  "auth": {
    "owner": {
      "groups": [],
      "users": [
        "local:test"
      ]
    }
  }
}'
```
</details>

---

### Rename a team

<details open>
 <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/rename</b></code> <code>(Rename a team)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |
> | Content-Type   |  required | string                   | Must be set to `application/json`                                     |
##### Body

> | name      |  type     | data type | description          |
> |-----------|-----------|-----------|----------------------|
> | name      | required  | string    | New name of the team |

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | `application/json` | See JSON example below |
| `400`     | application/json | See JSON 400 Example bellow |
| `401`     | text/plain; charset=utf-8 | not authorized  |
| `500`     | None | None |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{}
```
</details>
<details>
<summary>JSON Example for 400 Response</summary>

```json
{
  "errors": [
    "team: identifier cannot be an empty string"
  ]
}
```
</details>

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/team/rename \
  --header 'authorization: Bearer <access_token>' \
  --header 'content-type: application/json' \
  --data '{
  "name": "new-team-name"
}'
```
</details>

---

### Delete a team

<details open>
 <summary><code>DELETE</code> <code><b>/api/v1/teams/{team_name}</b></code> <code>(Remove a team)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |


##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:-------------------------:|:----------------------:|
| `204`     | None                      | None |
| `401`     | text/plain; charset=utf-8 | not authorized  |
| `404`     | None                      | None |

##### Example cURL
```shell
curl --request DELETE \
  --url http://localhost:8080/api/v1/teams/team \
  --header 'authorization: Bearer <access_token>'
```
</details>

---

### List builds for a team

<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/builds</b></code> <code>(List builds for a team)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |


##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:-------------------------:|:----------------------:|
| `200`     | application/json          | See JSON example below |
| `401`     | text/plain; charset=utf-8 | not authorized  |
| `404`     | None                      | None |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "id": 3,
    "team_name": "main",
    "name": "check",
    "status": "succeeded",
    "api_url": "/api/v1/builds/3",
    "resource_name": "1-minute",
    "pipeline_id": 1,
    "pipeline_name": "test",
    "start_time": 1763554980,
    "end_time": 1763554980
  }
]
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/builds \
  --header 'authorization: Bearer <access_token>'
```
</details>

---

### Create a build for a team

<details open>
 <summary><code>POST</code> <code><b>/api/v1/teams/{team_name}/builds</b></code> <code>(Create build for a team)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |
> | Content-Type   |  required | string                   | Must be set to `application/json`                                     |

##### Body

> | name        |  type     | data type | description                                      |
> |-------------|-----------|-----------|--------------------------------------------------|
> | task and id | required  | json      | Build configuration. Check example bellow |

<details>
<summary>JSON Example for Body</summary>

```json
{
  "id": "some-plan-id",
  "task": {
    "name": "simple-task",
    "config": {
      "platform": "linux",
      "image_resource": {
        "type": "registry-image",
        "source": {
          "repository": "busybox"
        }
      },
      "run": {
        "path": "sh",
        "args": ["-c", "echo 'Hello World'"]
      }
    }
  }
}
```
</details>

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:-------------------------:|:----------------------:|
| `201`     | application/json          | See JSON example below |
| `401`     | text/plain; charset=utf-8 | not authorized  |
| `400`     | None                      | None |

<details>
<summary>JSON Example for 201 Response</summary>

```json
{
  "id": 4,
  "team_name": "main",
  "name": "1",
  "status": "started",
  "api_url": "/api/v1/builds/4",
  "start_time": 1763562357
}
```
</details>

##### Example cURL
```shell
curl --request POST \
  --url http://localhost:8080/api/v1/teams/main/builds \
  --header 'authorization: Bearer <access_token>' \
  --header 'content-type: application/json' \
  --data '{
  "id": "some-plan-id",
  "task": {
    "name": "simple-task",
    "config": {
      "platform": "linux",
      "image_resource": {
        "type": "registry-image",
        "source": {
          "repository": "busybox"
        }
      },
      "run": {
        "path": "sh",
        "args": [
          "-c",
          "echo '\''Hello World'\''"
        ]
      }
    }
  }
}'
```
</details>

---

