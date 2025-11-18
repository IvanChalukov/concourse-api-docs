# Builds

#### List builds
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


#### Get build details

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