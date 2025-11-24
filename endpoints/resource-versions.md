# Resource Versions

### List resource versions

<details open> 
    <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resources/{resource_name}/versions</b></code> <code>(lists all resource versions)</code></summary>

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
    "id": 193,
    "version": {
      "id": "218981401",
      "tag": "v2.16.0",
      "timestamp": "2025-05-16T00:32:07Z"
    },
    "enabled": true
  }
]
```
</details>

##### Example cURL

```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/versions \
  --header 'authorization: Bearer <access_token>' 
```

</details>

---

### Clear all resource versions

<details open>
    <summary><code>DELETE</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resources/{resource_name}/versions</b></code> <code>(clears all resource versions)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `text/plain; charset=utf-8` | See response below     |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized         |


<details>
<summary>Response Example for 200 Response</summary>

```json
{
  "versions_removed": 1
}
```
</details>

##### Example cURL

```shell
curl --request DELETE \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/versions \
  --header 'authorization: Bearer <access_token>'
```

</details>

---

### Clear all resource type versions

<details open>
    <summary><code>DELETE</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resource-types/{resource_type_name}/versions</b></code> <code>(clears all resource type versions)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `text/plain; charset=utf-8` | See response below     |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized         |


<details>
<summary>Response Example for 200 Response</summary>

```json
{
  "versions_removed": 29
}
```
</details>

##### Example cURL

```shell
curl --request DELETE \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resource-types/github-release/versions \
  --header 'authorization: Bearer <access_token>'
```

</details>

---

### Get details for a resource version

<details open>
    <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resources/{resource_name}/versions/{resource_config_version_id}</b></code> <code>(gets details for a resource version)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | See JSON example below |
| `400`     | `text/plain; charset=utf-8` | None                   |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized         |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "id": 525,
  "version": {
    "id": "218981401",
    "tag": "v2.16.0",
    "timestamp": "2025-05-16T00:32:07Z"
  },
  "enabled": true
}
```
</details>

##### Example cURL

```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/versions/525 \
  --header 'authorization: Bearer <access_token>' 
```

</details>

---

### Enable a resource version

<details open>
    <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resources/{resource_name}/versions/{resource_config_version_id}/enable</b></code> <code>(enables a resource version)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | None                   |
| `400`     | `text/plain; charset=utf-8` | None                   |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized

##### Example cURL

```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/versions/525/enable \
  --header 'authorization: Bearer <access_token>'
```

</details>

---

### Disable a resource version

<details open>
    <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resources/{resource_name}/versions/{resource_config_version_id}/disable</b></code> <code>(disables a resource version)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | None                   |
| `400`     | `text/plain; charset=utf-8` | None                   |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized

##### Example cURL

```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/versions/525/disable \
  --header 'authorization: Bearer <access_token>'
```

</details>

---

### Pin a resource version
<details open>
    <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resources/{resource_name}/versions/{resource_config_version_id}/pin</b></code> <code>(pins a resource version)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | None                   |
| `400`     | `text/plain; charset=utf-8` | None                   |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized

##### Example cURL

```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/versions/525/pin \
  --header 'authorization: Bearer <access_token>'
```

</details>

---

### Unpin a resource version

<details open>
    <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resources/{resource_name}/unpin</b></code> <code>(unpins a resource version)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | None                   |
| `400`     | `text/plain; charset=utf-8` | None                   |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized

##### Example cURL

```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/unpin \
  --header 'authorization: Bearer <access_token>'
```

</details>

---

### Set pin comment on resource

<details open>
    <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resources/{resource_name}/pin-comment</b></code> <code>(sets pin comment on resource)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Request Body
```json
{
  "comment": "This is a pin comment"
}
```

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | None                   |
| `400`     | `text/plain; charset=utf-8` | None                   |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized

##### Example cURL

```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/pin-comment \
  --header 'authorization: Bearer <access_token>' \
  --header 'Content-Type: application/json' \
  --data '{
    "comment": "This is a pin comment"
  }'
```

</details>

---

### List builds with version as input

<details open>
    <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resources/{resource_name}/versions/{resource_config_version_id}/input_to</b></code> <code>(lists builds with version as input)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | See JSON example below |
| `400`     | `text/plain; charset=utf-8` | None                   |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized         |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "id": 591,
    "team_name": "main",
    "name": "1",
    "status": "succeeded",
    "api_url": "/api/v1/builds/591",
    "job_name": "testing/inout",
    "pipeline_id": 7,
    "pipeline_name": "inout",
    "start_time": 1763715474,
    "end_time": 1763715491,
    "created_by": "test"
  }
]
```
</details>

##### Example cURL

```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/versions/591/input_to \
  --header 'authorization: Bearer <access_token>'
```

</details>

---

### List builds with version as output

<details open>
    <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resources/{resource_name}/versions/{resource_config_version_id}/output_of</b></code> <code>(lists builds with version as output)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | See JSON example below |
| `400`     | `text/plain; charset=utf-8` | None                   |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized         |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "id": 591,
    "team_name": "main",
    "name": "1",
    "status": "succeeded",
    "api_url": "/api/v1/builds/591",
    "job_name": "testing/inout",
    "pipeline_id": 7,
    "pipeline_name": "inout",
    "start_time": 1763715474,
    "end_time": 1763715491,
    "created_by": "test"
  }
]
```
</details>

##### Example cURL

```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/versions/591/output_of \
  --header 'authorization: Bearer <access_token>'
```

</details>

---

### Get downstream resource causality

<details open>
    <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resources/{resource_name}/versions/{resource_config_version_id}/downstream</b></code> <code>(gets downstream resource causality)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | See JSON example below |
| `400`     | `text/plain; charset=utf-8` | None                   |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized         |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "jobs": [
    {
      "id": 14,
      "name": "testing/inout",
      "build_ids": [
        591
      ]
    }
  ],
  "builds": [
    {
      "id": 591,
      "name": "1",
      "job_id": 14,
      "status": "succeeded"
    }
  ],
  "resources": [
    {
      "id": 9,
      "name": "concourse-examples",
      "version_ids": [
        598
      ]
    }
  ],
  "resource_versions": [
    {
      "id": 598,
      "resource_id": 9,
      "version": {
        "ref": "254c2f62b8e6abc7af810e4f6e6bbe221c33d9be"
      },
      "build_ids": [
        591
      ]
    }
  ]
}
```

</details>

##### Example cURL

```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/versions/591/downstream \
  --header 'authorization: Bearer <access_token>'
```

</details>

---

### Get upstream resource causality

<details open>
    <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/resources/{resource_name}/versions/{resource_config_version_id}/upstream</b></code> <code>(gets upstream resource causality)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type                | Response Example       |
|:---------:|:----------------------------|:-----------------------|
| `200`     | `application/json`          | See JSON example below |
| `400`     | `text/plain; charset=utf-8` | None                   |
| `404`     | `text/plain; charset=utf-8` | None                   |
| `401`     | `text/plain; charset=utf-8` | not authorized

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "jobs": [
    {
      "id": 14,
      "name": "testing/inout",
      "build_ids": [
        591
      ]
    }
  ],
  "builds": [
    {
      "id": 591,
      "name": "1",
      "job_id": 14,
      "status": "succeeded"
    }
  ],
  "resources": [
    {
      "id": 8,
      "name": "otel-java-instrumentation-github-release",
      "version_ids": [
        525
      ]
    }
  ],
  "resource_versions": [
    {
      "id": 525,
      "resource_id": 8,
      "version": {
        "tag": "v2.16.0",
        "timestamp": "2025-05-16T00:32:07Z"
      },
      "build_ids": [
        591
      ]
    }
  ]
}
```

</details>

##### Example cURL

```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/versions/591/upstream \
  --header 'authorization: Bearer <access_token>'
```

</details>
