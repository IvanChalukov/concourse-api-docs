# Pipelines

### Get pipeline configuration
<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/config</b></code> <code>(retrieves the configuration of a pipeline)</code></summary>

##### Headers

| name          | type     | data type | description                                 |
|---------------|----------|-----------|---------------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token    |

##### Responses

| HTTP Code | Content-Type                | Response Example          |
|:---------:|:----------------------------|:--------------------------|
| `200`     | `application/json`          | See JSON example below    |
| `404`     | `text/plain; charset=utf-8` | None                      |
| `401`     | `text/plain; charset=utf-8` | not authorized            |
| `500`     | `text/plain; charset=utf-8` | error message             |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
    "config": {
        "groups": [],
        "var_sources": [],
        "resources": [],
        "resource_types": [],
        "prototypes": [],
        "jobs": [],
        "display": {}
    }
}
```
</details>                                       

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/update-pipeline \
  --header 'authorization: Bearer <access_token>' \
  --header 'content-type: application/x-www-form-urlencoded'
```
</details>
---

### Create/Update pipeline configuration
<details open>
 <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/config</b></code> <code>(create/updates the configuration of a pipeline)</code></summary>

##### Headers

| name                        | type     | data type | description                                                                                                                                           |
|-----------------------------|----------|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authorization               | required | string    | Bearer auth header with the access token                                                                                                              |
| Content-Type                | required | string    | Must be set to `application/json`                                                                                                                     |
| X-Concourse-Config-Version  | optional | integer   | The version of the pipeline configuration being submitted. If provided, the update will only succeed if the current version matches this value. This helps prevent conflicting updates. |



##### Body
```json
{
    "config": {
        "groups": [],
        "var_sources": [],
        "resources": [],
        "resource_types": [],
        "prototypes": [],
        "jobs": [], // Required
        "display": {}
    }
}
```

##### Flow
1. If the pipeline does not exist, it will be created.
2. If the pipeline exists, its configuration will be updated.


##### Responses
| HTTP Code | Content-Type                | Response Example  |
|:---------:|:---------------------------|:-------------------|
| `200`     | `application/json`          | None              |
| `201`     | `application/json`          | None              |
| `401`     | `text/plain; charset=utf-8` | not authorized    |
| `500`     | `text/plain; charset=utf-8` | error message     |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/xss/config \
  --header 'authorization: Bearer <access_token>' \
  --header 'content-type: application/json' \
  --header 'x-concourse-config-version: 53' \
  --data '{
  "jobs": [
    {
      "name": "hello-world-job1",
      "plan": [
        {
          "config": {
            "platform": "linux",
            "image_resource": {
              "name": "",
              "type": "registry-image",
              "source": {
                "repository": "alpine",
                "tag": "latest"
              }
            },
            "run": {
              "path": "echo",
              "args": [
                "Hello world!"
              ]
            }
          },
          "task": "hello-world-task"
        }
      ]
    }
  ]
}'
```

</details>
---

### List all pipelines
<details open>
 <summary><code>GET</code> <code><b>/api/v1/pipelines</b></code> <code>(lists all pipelines across all teams)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|------------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses
| HTTP Code | Content-Type                | Response Example        |
|:---------:|:---------------------------|:-------------------------|
| `200`     | `application/json`          | See JSON example below  |
| `404`     | `text/plain; charset=utf-8` | None                    |
| `401`     | `text/plain; charset=utf-8` | not authorized          |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "id": 26,
    "name": "alpha",
    "paused": true,
    "paused_by": "test",
    "paused_at": 1763450523,
    "public": false,
    "archived": false,
    "team_name": "alpha",
    "last_updated": 1763446515
  },
  ...
]
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/pipelines \
  --header 'authorization: Bearer <access_token>' 
```

</details>
---

### List pipelines for team
<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines</b></code> <code>(lists all pipelines for a specific team)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              | 

##### Responses
| HTTP Code | Content-Type                | Response Example        |
|:---------:|:---------------------------|:-------------------------|
| `200`     | `application/json`          | See JSON example below  |
| `404`     | `text/plain; charset=utf-8` | None                    |
| `401`     | `text/plain; charset=utf-8` | not authorized          |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "id": 26,
    "name": "alpha",
    "paused": true,
    "paused_by": "test",
    "paused_at": 1763450523,
    "public": false,
    "archived": false,
    "team_name": "alpha",
    "last_updated": 1763446515
  },
  ...
]
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines \
  --header 'authorization: Bearer <access_token>'
```

</details>
---

### Get pipeline details

<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}</b></code> <code>(retrieves details of a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                              |
> |----------------|-----------|-------------------------|------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token |           

##### Responses
| HTTP Code | Content-Type                | Response Example        |
|:---------:|:----------------------------|:------------------------|
| `200`     | `application/json`          | See JSON example below  |
| `404`     | `text/plain; charset=utf-8` | None                    |
| `401`     | `text/plain; charset=utf-8` | not authorized          |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "id": 26,
  "name": "alpha",
  "paused": true,
  "paused_by": "test",
  "paused_at": 1763450523,
  "public": false,
  "archived": false,
  "team_name": "alpha",
  "last_updated": 1763446515
}
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/alpha \
  --header 'authorization: Bearer <access_token>'
```

</details>
---

### Delete a pipeline

<details open>
 <summary><code>DELETE</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}</b></code> <code>(deletes a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                               |
> |----------------|-----------|-------------------------|-------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token. |

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `204`     | `application/json`          | None                   |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized         |

##### Example cURL
```shell
curl --request DELETE \
  --url http://localhost:8080/api/v1/teams/main/pipelines/alpha \
  --header 'authorization: Bearer <access_token>'
```

</details>
---

### Set pipeline ordering for a team

<details open>
 <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/ordering</b></code> <code>(sets the order of pipelines for a team)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |                 

##### Request Body

```json
[
  "xs1s1",
  "xss",
  "xs1s",
  "xss2"
]
```

##### Responses
| HTTP Code | Content-Type                | Response Example  |
|:---------:|:----------------------------|:------------------|
| `200`     | `application/json`          | None              |
| `404`     | `text/plain; charset=utf-8` | None              |
| `401`     | `text/plain; charset=utf-8` | not authorized    |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/ordering \
  --header 'authorization: Bearer <access_token>' \
  --header 'content-type: application/json' \
  --data '[
  "xs1s1",
  "xss",
  "xs1s",
  "xss2"
]'
```

</details>
--- 

### Set pipeline ordering within a group

<details open>
 <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/ordering</b></code> <code>(sets the order of jobs within a pipeline group)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Request Body

```json
[
    {
        "number": 1
    },
    {
        "number": 2
    },
    {
        "number": 3
    },
    {
        "number": 4
    }
]
```

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | None                   |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized         |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/xss/ordering \
  --header 'authorization: Bearer <access_token>' \
  --header 'content-type: application/json' \
  --data '[
    {
        "number": 1
    },
    { 
        "number": 2
    },
    {
        "number": 3
    },
    {
        "number": 4
    }
]'
```
</details>
---

### Pause a pipeline

<details open>
 <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/pause</b></code> <code>(pauses a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example |
|:---------:|:----------------------------|:-----------------|
| `200`     | `application/json`          | None             |
| `404`     | `text/plain; charset=utf-8` | None             |
| `401`     | `text/plain; charset=utf-8` | not authorized   |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/alpha/pause \
  --header 'authorization: Bearer <access_token>'
```

</details>
---

### Archive a pipeline

<details open>
 <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/archive</b></code> <code>(archives a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example |
|:---------:|:----------------------------|:-----------------|
| `200`     | `application/json`          | None             |
| `404`     | `text/plain; charset=utf-8` | None             |
| `401`     | `text/plain; charset=utf-8` | not authorized   |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/alpha/archive \
  --header 'authorization: Bearer <access_token>'
```

</details>
---

### Unpause a pipeline
<details open>
 <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/unpause</b></code> <code>(unpauses a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example |
|:---------:|:----------------------------|:-----------------|
| `200`     | `application/json`          | None             |
| `404`     | `text/plain; charset=utf-8` | None             |
| `401`     | `text/plain; charset=utf-8` | not authorized   |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/alpha/unpause \
  --header 'authorization: Bearer <access_token>'
```

</details>
---

### Expose a pipeline
<details open>
 <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/expose</b></code> <code>(exposes a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                             |

##### Responses
| HTTP Code | Content-Type                | Response Example |
|:---------:|:----------------------------|:-----------------|
| `200`     | `application/json`          | None             |
| `404`     | `text/plain; charset=utf-8` | None             |
| `401`     | `text/plain; charset=utf-8` | not authorized   |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/alpha/expose \
  --header 'authorization: Bearer <access_token>'
```

</details>
---

### Hide a pipeline
<details open>
 <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/hide</b></code> <code>(hides a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example |
|:---------:|:----------------------------|:-----------------|
| `200`     | `application/json`          | None             |
| `404`     | `text/plain; charset=utf-8` | None             |
| `401`     | `text/plain; charset=utf-8` | not authorized   |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/alpha/hide \
  --header 'authorization: Bearer <access_token>'
```

</details>
---

### Get pipeline versions database
<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/versions-db</b></code> <code>(retrieves the versions database of a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | See JSON example below |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized         |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "Jobs": [
    {
      "Name": "hello-world-job",
      "ID": 2
    }
  ],
  "Resources": [],
  "ResourceVersions": [],
  "BuildOutputs": [],
  "BuildInputs": [],
  "BuildReruns": []
}
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/alpha/versions-db \
  --header 'authorization: Bearer <access_token>'
```

</details>
---

### Rename a pipeline
<details open>
 <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/rename</b></code> <code>(renames a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Body
```json
{
  "name": "new-pipeline-name"
}
```

##### Responses
| HTTP Code | Content-Type                | Response Example |
|:---------:|:----------------------------|:-----------------|
| `200`     | `application/json`          | None             |
| `404`     | `text/plain; charset=utf-8` | None             |
| `401`     | `text/plain; charset=utf-8` | not authorized   |
| `500`     | `text/plain; charset=utf-8` | None             |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/old-pipeline-name/rename \
  --header 'authorization: Bearer <access_token>' \
  --header 'content-type: application/json' \
  --data '{
  "name": "xss2"
}'
```

</details>
---

### List builds for a pipeline
<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/builds</b></code> <code>(lists all builds for a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | See JSON example below |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized         |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "id": 1,
    "team_name": "main",
    "name": "1",
    "status": "started",
    "api_url": "/api/v1/builds/1",
    "job_name": "hello-world-job1",
    "pipeline_id": 3,
    "pipeline_name": "xss2",
    "start_time": 1763629549,
    "created_by": "test"
  }
]
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/alpha/builds \
  --header 'authorization: Bearer <access_token>'
```

</details>
---

### Create a build for a pipeline
<details>
  <summary><code>POST</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/builds</b></code> <code>(creates a new build for a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Body
```json
{
  "job": "hello-world-job1"
}
```

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `201`     | `application/json`          | See JSON example below |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized         |
| `500`     | `text/plain; charset=utf-8` | None                   |

##### Example cURL
```shell
curl --request POST \
  --url http://localhost:8080/api/v1/teams/main/pipelines/alpha/builds \
  --header 'authorization: Bearer <access_token>' \
  --header 'content-type: application/json' \
  --data '{
  "job": "hello-world-job1"
}'
```

</details>
---

### Get pipeline status badge (SVG)
<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/badge</b></code> <code>(retrieves the status badge SVG for a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example |
|:---------:|:----------------------------|:-----------------|
| `200`     | `image/svg+xml`             | SVG content      |
| `404`     | `text/plain; charset=utf-8` | None             |
| `401`     | `text/plain; charset=utf-8` | not authorized   |

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/alpha/badge \
  --header 'authorization: Bearer <access_token>'
```

</details>
---