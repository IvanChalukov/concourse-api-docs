# Containers

### List containers for a team

<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/containers</b></code> <code>(retrieves the containers in a team)</code></summary>

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
[
  {
    "id": "1b38510f-fde4-4709-981e-42789b928310",
    "worker_name": "e98fdeb3d200",
    "state": "created",
    "type": "check",
    "step_name": "1-minute",
    "pipeline_id": 2,
    "pipeline_name": "test",
    "build_name": "check",
    "working_directory": "/tmp/build/check"
  }
]
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/containers \
  --header 'authorization: Bearer <token>'
```
</details>

---

### Get container details
<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/containers/{id}</b></code> <code>(Gets container details)</code></summary>

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
  "id": "1b38510f-fde4-4709-981e-42789b928310",
  "worker_name": "e98fdeb3d200",
  "state": "created",
  "type": "check",
  "step_name": "1-minute",
  "pipeline_id": 2,
  "pipeline_name": "test",
  "build_name": "check",
  "working_directory": "/tmp/build/check"
}
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/containers \
  --header 'authorization: Bearer <token>'
```
</details>

---

### Hijack a container
<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/containers/{id}/hijack</b></code> <code>(Hijack a container)</code></summary>

>#### Not a standard HTTP endpoint, requires WebSocket to hijack the container.
</details>

---

### List destroying containers
<details open>
 <summary><code>GET</code> <code><b>/api/v1/containers/destroying</b></code> <code>(List destroying containers)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Query Parameters
> | name        |  type     | data type               | description                                                           |
> |-------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | worker_name |  required | string                  | The name of the worker to list destroying containers for                 |

##### Responses

| HTTP Code | Content-Type              | Response Example       |
|:---------:|:-------------------------:|:----------------------:|
| `200`     | `application/json`        | See JSON example below |
| `400`     | None                      | None                   |
| `401`     | text/plain; charset=utf-8 | not authorized         |
<details>
<summary>JSON Example for 200 Response.</summary>

```json
[
  "f698ca2f-251a-47a5-8ee6-a849cafd0111"
]
```
> Will be `[]` if no containers are being destroyed or no such worker exists.
</details>

```shell
curl --request GET \
  --url 'http://localhost:8080/api/v1/containers/destroying?worker_name=e98fdeb3d200' \
  --header 'authorization: Bearer <token>'
```
</details>

---

### Report worker containers
<details open>
 <summary><code>PUT</code> <code><b>/api/v1/containers/report</b></code> <code>(Workers provide their current containers)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |
> | Content-Type   |  required | string                   | Must be set to `application/json`                                     |

##### Query Parameters
> | name        |  type     | data type               | description                                                           |
> |-------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | worker_name |  required | string                  | The name of the worker to list destroying containers for                 |

##### Body
> | name            |  type     | data type | description                                   |
> |-----------------|-----------|-----------|-----------------------------------------------|
> | containers list | required  | json      | List of containers on worker. Example bellow  |

<details>
<summary>JSON Example for Body</summary>

```json
[
  "container-handle-1",
  "container-handle-2"
]
```
</details>

##### Responses
| HTTP Code | Content-Type              | Response Example       |
|:---------:|:-------------------------:|:----------------------:|
| `204`     | `application/json`        | None                   |
| `400`     | `application/json`        | None                   |
| `401`     | text/plain; charset=utf-8 | not authorized         |
| `404`     | `application/json`        | None                   |
| `500`     | `application/json`        | None                   |

##### Example cURL
```shell
curl --request PUT \
  --url 'http://localhost:8080/api/v1/containers/report?worker_name=e98fdeb3d200' \
  --header 'authorization: Bearer <token>' \
  --header 'content-type: application/json' \
  --data '[
  "container-handle-1",
  "container-handle-2"
]'
```
</details>

---