# Pipelines

### Pipeline config

#### Get pipeline configuration
<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/config</b></code> <code>(retrieves the configuration of a pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses

| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:-------------------------------|
| `200`     | `application/json` | See JSON example below          |
| `404`     | text/plain; charset=utf-8 | None                           |
| `401`     | text/plain; charset=utf-8 | not authorized                           |
| `500`     | text/plain; charset=utf-8 | None                           |

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
  --header 'authorization: Bearer <token>' \
  --header 'content-type: application/x-www-form-urlencoded'
```
</details>

#### Create/Update pipeline configuration
<details open>
 <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/config</b></code> <code>(create/updates the configuration of a pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token
> | Content-Type   |  required | string                  | Must be set to `application/json`                                     |
> | X-Concourse-Config-Version |  optional | integer         | The version of the pipeline configuration being submitted. If provided, the update will only succeed if the current version matches this value. This helps prevent conflicting updates. |



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
| HTTP Code | Content-Type       | Response Example                |
|:---------:|:------------------|:-------------------------------|
| `200`     | `application/json` | None          |
| `201`     | `application/json` | None          |
| `401`     | text/plain; charset=utf-8  | not authorized                           |
| `500`     | text/plain; charset=utf-8  | error message                           |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/teams/main/pipelines/xss/config \
  --header 'authorization: Bearer <token>' \
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