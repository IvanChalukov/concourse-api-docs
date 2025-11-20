# Resources

### List all resources

<details>
 <summary><code>GET</code> <code><b>/api/v1/resources</b></code> <code>(lists all resources across pipelines)</code></summary>

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `200`     | `application/json` | See JSON example below          |  
| `401`     | text/plain; charset=utf-8 | not authorized           |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "name": "otel-java-instrumentation-github-release",
    "pipeline_id": 6,
    "pipeline_name": "inout",
    "team_name": "main",
    "type": "github-release",
    "last_checked": 1763631812,
    "icon": "github",
    "build": {
      "id": 8,
      "name": "check",
      "status": "succeeded",
      "start_time": 1763631809,
      "end_time": 1763631812,
      "team_name": "main",
      "pipeline_id": 6,
      "pipeline_name": "inout",
      "plan": {
        "id": "691b2f2b",
        "check": {
          "name": "otel-java-instrumentation-github-release",
          "type": "github-release"
        }
      }
    }
  }
]
```

</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/resources \
  --header 'authorization: bearer <token>'
```

</details>
---

### List resources in a pipeline

<details>
 <summary><code>GET</code> <code><b>/api/v1/teams/:team_name/pipelines/:pipeline_name/resources</b></code> <code>(lists resources in a pipeline)</code></summary>

##### Headers
> | name           | type     | data type | description                              |
> |----------------|----------|-----------|------------------------------------------|
> | Authorization  | required | string    | Bearer auth header with the access token |

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `200`     | `application/json` | See JSON example below          |  
| `401`     | text/plain; charset=utf-8 | not authorized                           |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "name": "otel-java-instrumentation-github-release",
    "pipeline_id": 6,
    "pipeline_name": "inout",
    "team_name": "main",
    "type": "github-release",
    "last_checked": 1763632013,
    "icon": "github",
    "build": {
      "id": 11,
      "name": "check",
      "status": "succeeded",
      "start_time": 1763632012,
      "end_time": 1763632013,
      "team_name": "main",
      "pipeline_id": 6,
      "pipeline_name": "inout",
      "plan": {
        "id": "691b2f2d",
        "check": {
          "name": "otel-java-instrumentation-github-release",
          "type": "github-release"
        }
      }
    }
  }
]
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources \
    --header 'authorization: bearer <token>'
```

</details>
---

### List shared info for a resource

<details>
 <summary><code>GET</code> <code><b>/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/shared</b></code> <code>(lists shared info for a resource)</code></summary>
 
##### Headers
> | name           | type     | data type | description                              |
> |----------------|----------|-----------|------------------------------------------|
> | Authorization  | required | string    | Bearer auth header with the access token |

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `200`     | `application/json` | See JSON example below          |  
| `401`     | text/plain; charset=utf-8 | not authorized           |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "resources": [
    {
      "name": "otel-java-instrumentation-github-release",
      "pipeline_name": "inout",
      "team_name": "main"
    }
  ],
  "resource_types": null
}
```

</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/shared \
  --header 'authorization: bearer <token>'
```

</details>
---

### List shared info for a resource type

<details>
 <summary><code>GET</code> <code><b>/api/v1/teams/:team_name/pipelines/:pipeline_name/resource-types/:resource_type_name/shared</b></code> <code>(lists shared info for a resource type)</code></summary>

##### Headers
> | name           | type     | data type | description                              |
> |----------------|----------|-----------|------------------------------------------|
> | Authorization  | required | string    | Bearer auth header with the access token |

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | text/plain; charset=utf-8 | not authorized           |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "name": "rss",
    "type": "registry-image",
    "source": {
      "repository": "suhlig/concourse-rss-resource",
      "tag": "latest"
    }
  }
]
```

</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resource-types/rss/shared \
  --header 'authorization: bearer <token>'
```

</details>
---

### List resource types in a pipeline
<details>
 <summary><code>GET</code> <code><b>/api/v1/teams/:team_name/pipelines/:pipeline_name/resource-types</b></code> <code>(lists resource types in a pipeline)</code></summary>

##### Headers
> | name           | type     | data type | description                              |
> |----------------|----------|-----------|------------------------------------------|
> | Authorization  | required | string    | Bearer auth header with the access token |

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | text/plain; charset=utf-8 | not authorized           |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "resource_types": [
    {
      "name": "rss",
      "pipeline_name": "inout",
      "team_name": "main"
    }
  ]
}
```

</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resource-types \
  --header 'authorization: bearer <token>'
```

</details>
---

### Get resource details
<details>
 <summary><code>GET</code> <code><b>/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name</b></code> <code>(get resource details)</code></summary>

##### Headers
> | name           | type     | data type | description                              |
> |----------------|----------|-----------|------------------------------------------|
> | Authorization  | required | string    | Bearer auth header with the access token |

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | text/plain; charset=utf-8 | not authorized           |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "name": "dinosaur-comics",
  "pipeline_id": 6,
  "pipeline_name": "inout",
  "team_name": "main",
  "type": "rss",
  "last_checked": 1763646232,
  "build": {
    "id": 204,
    "name": "check",
    "status": "failed",
    "start_time": 1763646231,
    "end_time": 1763646232,
    "team_name": "main",
    "pipeline_id": 6,
    "pipeline_name": "inout",
    "plan": {
      "id": "691b2fed",
      "check": {
        "name": "dinosaur-comics",
        "type": "rss",
        "image_get_plan": {
          "id": "691b2fed/image-get",
          "get": {
            "name": "rss",
            "type": "registry-image"
          }
        },
        "image_check_plan": {
          "id": "691b2fed/image-check",
          "check": {
            "name": "rss",
            "type": "registry-image"
          }
        }
      }
    }
  }
}
```

</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/dinosaur-comics \
  --header 'authorization: bearer <token>'
```

</details>
---

### Trigger resource check
<details>
 <summary><code>POST</code> <code><b>/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/check</b></code> <code>(triggers resource check)</code></summary>

##### Headers
> | name           | type     | data type | description                              |
> |----------------|----------|-----------|------------------------------------------|
> | Authorization  | required | string    | Bearer auth header with the access token |

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | text/plain; charset=utf-8 | not authorized           |

##### Request Body
> | name    | type     | data type | description                                                   |
> |---------|----------|-----------|---------------------------------------------------------------|
> | from    | optional | array     | Specific version to check from, or empty object/null for latest |
> | shallow | optional | boolean   | If true, only the latest version will be checked              |


<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "id": 210,
  "team_name": "main",
  "name": "check",
  "status": "started",
  "api_url": "/api/v1/builds/210",
  "resource_name": "otel-java-instrumentation-github-release",
  "pipeline_id": 6,
  "pipeline_name": "inout",
  "start_time": 1763646496
}
```

</details>

##### Example cURL
```shell
curl --request POST \
  --url http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/check \
  --header 'authorization: Bearer <token>' \
  --header 'content-type: application/json' \
  --data '{
  "from": null
}'
```

</details>
---

### Trigger resource check via webhook
<details>
 <summary><code>POST</code> <code><b>/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/check/webhook</b></code> <code>(triggers resource check via webhook)</code></summary>

##### Headers
> | name           | type     | data type | description                              |
> |----------------|----------|-----------|------------------------------------------|
> | Authorization  | required | string    | Bearer auth header with the access token |

##### Query Parameters
> | name    | type     | data type | description                                                   |
> |---------|----------|-----------|---------------------------------------------------------------|
> | webhook_token | required | string | The webhook token configured for the resource |

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | text/plain; charset=utf-8 | not authorized           |    

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "id": 210,
  "team_name": "main",
  "name": "check",
  "status": "started",
  "api_url": "/api/v1/builds/210",
  "resource_name": "otel-java-instrumentation-github-release",
  "pipeline_id": 6,
  "pipeline_name": "inout",
  "start_time": 1763646496
}
```

</details>

##### Example cURL
```shell
curl --request POST \
  --url 'http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/otel-java-instrumentation-github-release/check/webhook?webhook_token=<webhook_token>' \
  --header 'authorization: Bearer <token>'
```

</details>
---

### Trigger resource type check
<details>
 <summary><code>POST</code> <code><b>/api/v1/teams/:team_name/pipelines/:pipeline_name/resource-types/:resource_type_name/check</b></code> <code>(triggers resource type check)</code></summary>

##### Headers
> | name           | type     | data type | description                              |
> |----------------|----------|-----------|------------------------------------------|
> | Authorization  | required | string    | Bearer auth header with the access token |


##### Request Body
> | name    | type     | data type | description                                                        |
> |---------|----------|-----------|--------------------------------------------------------------------|
> | from    | optional | array     | Specific version to check from, or empty object/null for latest    |
> | shallow | optional | boolean   | If true, only the latest version will be checked                   |


##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | text/plain; charset=utf-8 | not authorized           |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "id": 224,
  "team_name": "main",
  "name": "check",
  "status": "started",
  "api_url": "/api/v1/builds/224",
  "pipeline_id": 6,
  "pipeline_name": "inout",
  "start_time": 1763647500
}
```

</details>

##### Example cURL
```shell
curl --request POST \
  --url 'http://localhost:8080/api/v1/teams/main/pipelines/inout/resource-types/rss/check' \
  --header 'authorization: Bearer <token>'
```

</details>

### Trigger prototype check
<details>
 <summary><code>POST</code> <code><b>/api/v1/teams/:team_name/pipelines/:pipeline_name/prototypes/:prototype_name/check</b></code> <code>(triggers prototype check)</code></summary>

##### Headers
> | name           | type     | data type | description                              |
> |----------------|----------|-----------|------------------------------------------|
> | Authorization  | required | string    | Bearer auth header with the access token |

##### Request Body
> | name    | type     | data type | description                                                   |
> |---------|----------|-----------|---------------------------------------------------------------|
> | from    | optional | array     | Specific version to check from, or empty object/null for latest |
> | shallow | optional | boolean   | If true, only the latest version will be checked              |

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `401`     | text/plain; charset=utf-8 | not authorized           |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "id": 224,
  "team_name": "main",
  "name": "check",
  "status": "started",
  "api_url": "/api/v1/builds/224",
  "pipeline_id": 6,
  "pipeline_name": "inout",
  "start_time": 1763647500
}
```

</details>

##### Example cURL
```shell
curl --request POST \
  --url 'http://localhost:8080/api/v1/teams/main/pipelines/inout/prototypes/otel-java-instrumentation-github-release/check' \
  --header 'authorization: Bearer <token>'
```

</details>
---

### Clear resource cache
<details>
 <summary><code>DELETE</code> <code><b>/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/cache</b></code> <code>(clears resource cache)</code></summary>

##### Headers
> | name           | type     | data type | description                              |
> |----------------|----------|-----------|------------------------------------------|
> | Authorization  | required | string    | Bearer auth header with the access token |

##### Responses
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:---------------------------------|
| `204`     | `application/json` | See JSON example below          |
| `401`     | text/plain; charset=utf-8 | not authorized           |

<details>
<summary>JSON Example for 204 Response</summary>

```json
{
  "caches_removed": 0
}
```

</details>

##### Example cURL

```shell
curl --request DELETE \
  --url 'http://localhost:8080/api/v1/teams/main/pipelines/inout/resources/rss/cache' \
  --header 'authorization: Bearer <token>'
```

</details>
