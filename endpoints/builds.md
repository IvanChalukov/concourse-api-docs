# Builds

### List builds
<details>
    <summary><code>GET</code> <code><b>/builds</b></code> <code>(lists all builds across all teams and pipelines)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Query Parameters
> | name      |  type     | data type               | description                                                           |
> |-----------|-----------|-------------------------|-----------------------------------------------------------------------|
> | limit     |  optional | integer                 | Maximum number of builds to return (default: 100)          |
> | from      |  optional | integer                 | Return builds with ID less than this value (for pagination)           |
> | to        |  optional | integer                 | Return builds with ID greater than this value (for pagination)        |
> | timestamps |  optional | boolean                 | If true, `from` and `to` are treated as timestamps instead of IDs (default: false)  |

> None

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:-------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | `application/json` | not authorized                           |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
    {
        "id": 298719,
        "team_name": "main-team",
        "name": "build-123",
        "status": "succeeded",
        "api_url": "http://localhost:8080/api/v1/builds/298719",
        "comment": "Build completed successfully",
        "job_name": "deploy-job",
        "resource_name": "git-repo",
        "pipeline_id": 42,
        "pipeline_name": "main-pipeline",
        "pipeline_instance_vars": {},
        "start_time": 1718000000,
        "end_time": 1718000600,
        "reap_time": 1718001200,
        "rerun_number": 1,
        "rerun_of": {},
        "created_by": "user123"
    }
]
```
</details>  

##### Example cURL

```shell
curl --request GET \
  --url http://localhost:8080/api/v1/builds \
  --header 'authorization: Bearer <token>' \
```
</details>

---

### Get build details

<details>
    <summary><code>GET</code> <code><b>/builds/{build_id}</b></code> <code>(retrieves details of a specific build)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:-------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | `application/json` | not authorized                           |
| `404`     | `application/json` | build not found                           |

<details>
<summary>JSON Example for 200 Response</summary>
```json
{
    "id": 298719,
    "team_name": "main-team",
    "name": "build-123",
    "status": "succeeded",
    "api_url": "http://localhost:8080/api/v1/builds/298719",
    "comment": "Build completed successfully",
    "job_name": "deploy-job",
    "resource_name": "git-repo",
    "pipeline_id": 42,
    "pipeline_name": "main-pipeline",
    "pipeline_instance_vars": {
    },
    "start_time": 1718000000,
    "end_time": 1718000600,
    "reap_time": 1718001200,
    "rerun_number": 1,
    "rerun_of": {
    },
    "created_by": "user123"
}
```
</details>

##### Example cURL

```shell
curl --request GET \
  --url https://concourse.cf.concourse-dev.concourse-azure.sapcloud.io/api/v1/builds/298719 \
  --header 'authorization: Bearer <token>' 
```
</details>

---

### Get build plan

<details>
    <summary><code>GET</code> <code><b>/builds/{build_id}/plan</b></code> <code>(retrieves the build plan for a specific build)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:-------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | `application/json` | not authorized                           |
| `404`     | `application/json` | build not found                           |

<details>
<summary>JSON Example for 200 Response</summary>
```json
{
    "schema": "exec.v2",
    "plan": {
        "id": "68fa6edf",
        "do": [ ... ]
    }
}
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/builds/123/plan \
  --header 'authorization: Bearer <token>' 
```
</details>

---

### Stream build events

<details>
    <summary><code>GET</code> <code><b>/builds/{build_id}/events</b></code> <code>(streams build events for a specific build)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:-------------------------------|
| `200`     | `text/event-stream` | See ES(event-stream) example below - in text/event-stream; charset=utf-8 |
| `401`     | `application/json` | not authorized                           |
| `404`     | `application/json` | build not found                           |

<details>
<summary>Event Stream Example for 200 Response</summary>

```text
id: 0
event: event
data: {
    "data": {
        "status": "started",
        "time": 1763467283
    },
    "event": "status",
    "version": "1.0",
    "event_id": "0"
}

id: 1
event: event
data: {
    "data": {
        "origin": {
            "id": "690ecb6c"
        },
        "time": 1763467283
    },
    "event": "initialize-get",
    "version": "2.0",
    "event_id": "1"
}

id: 2
event: event
data: {
    "data": {
        "origin": {
            "id": "690ecb68"
        },
        "time": 1763467283
    },
    "event": "initialize-get",
    "version": "2.0",
    "event_id": "2"
}
```

</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/builds/123/events \
  --header 'authorization: Bearer <token>'
```
</details>

---

### Get build resources

<details>
    <summary onclick="this.open = !this.open" style="cursor:pointer;"><code>GET</code> <code><b>/builds/{build_id}/resources</b></code> <code>(retrieves resources associated with a specific build)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:-------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | `application/json` | not authorized                           |
| `404`     | `application/json` | build not found                           |

<details>
<summary>JSON Example for 200 Response</summary>
```json
{
  "inputs": [
    {
      "name": "some-resource",
      "version": {
        "ref": "6e181c354d20297c3b862ed3d48fc670ff06c755"
      },
      "pipeline_id": 9,
      "first_occurrence": true
    },
    {
      "name": "some-other-resource",
      "version": {
        "ref": "0d712832ee7688429f4bd6180202dcaab69c9a05"
      },
      "pipeline_id": 9,
      "first_occurrence": true
    }
  ],
  "outputs": []
}
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/builds/123/resources \
  --header 'authorization: Bearer <token>'
```
</details>

---

### Abort build

<details>
    <summary><code>PUT</code> <code><b>/builds/{build_id}/abort</b></code> <code>(aborts a specific build)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `204`     | `application/json` | None                            |
| `401`     | `application/json` | not authorized                  |
| `404`     | `application/json` | build not found                 |


##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/builds/123/abort \
  --header 'authorization: Bearer <token>'
```
</details>

---

### Get build preparation status

<details>
    <summary><code>GET</code> <code><b>/builds/{build_id}/preparation</b></code> <code>(retrieves the preparation status of a specific build)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:-------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | `application/json` | not authorized                  |
| `404`     | `application/json` | build not found                 |

<details>
<summary>JSON Example for 200 Response</summary>
```json
{
  "build_id": 301596,
  "paused_pipeline": "not_blocking",
  "paused_job": "not_blocking",
  "max_running_builds": "not_blocking",
  "inputs": {},
  "inputs_satisfied": "not_blocking",
  "missing_input_reasons": {}
}
```

</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/builds/123/preparation \
  --header 'authorization: Bearer <token>'
```
</details>

---

### Get build artifacts

<details>
    <summary><code>GET</code> <code><b>/builds/{build_id}/artifacts</b></code> <code>(lists artifacts produced by a specific build)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:-------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | `application/json` | not authorized                  |
| `404`     | `application/json` | build not found                 |

<details>
<summary>JSON Example for 200 Response</summary>
```json
[
    {
        "id": 1,
        "name": "artifact-name",
        "build_id": 123,
        "created_at": "2024-06-13T12:34:56Z",
        "volume": {}
    }
]
```
</details>

##### Example cURL
```shell
curl --request GET \
    --url http://localhost:8080/api/v1/builds/123/artifacts \
    --header 'authorization: Bearer <token>'
```
</details>

---

### Add comment to build

<details>
    <summary><code>PUT</code> <code><b>/builds/{build_id}/comment</b></code> <code>(adds a comment to a specific build)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token
> | Content-Type   |  required | string                  | Must be set to `application/json`                                     |

##### Body
```json
{
    "comment": "This is a comment on the build."
}
```

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `200`     | `application/json` | None                            |
| `401`     | `application/json` | not authorized                  |
| `404`     | `application/json` | build not found                 |    

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/builds/301596/comment \
  --header 'authorization: Bearer JQ1kjCoXQMyPlhieYQl/efPVFXI+vRxpAAAAAA' \
  --header 'content-type: application/json' \
  --data '{
  "comment": "test-api"
}'
```
</details>