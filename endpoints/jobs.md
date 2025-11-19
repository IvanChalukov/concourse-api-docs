# Jobs

### List all jobs
<details open>
    <summary><code>GET</code> <code><b>/api/v1/jobs</b></code> <code>(lists all jobs)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type                | Response                                                                                                   |
|-----------|-----------------------------|------------------------------------------------------------------------------------------------------------|
| `200`     | `application/json`          | See JSON example below  |
| `401`     | `application/json`          | not authorized                                                                                             |

<details>
<summary>JSON Example for 200 Response</summary>
```json
[
  {
    "id": 393,
    "name": "test-containerd-issue-iac",
    "team_name": "product-cf",
    "pipeline_id": 17,
    "pipeline_name": "test_containerd_issue_iac",
    "finished_build": {
      "id": 301596,
      "name": "10",
      "status": "aborted",
      "start_time": 1763484646,
      "end_time": 1763484663,
      "team_name": "product-cf",
      "pipeline_id": 17,
      "pipeline_name": "test_containerd_issue_iac",
      "job_name": "test-containerd-issue-iac"
    },
    "transition_build": {
      "id": 301591,
      "name": "9",
      "status": "aborted",
      "start_time": 1763484570,
      "end_time": 1763484580,
      "team_name": "product-cf",
      "pipeline_id": 17,
      "pipeline_name": "test_containerd_issue_iac",
      "job_name": "test-containerd-issue-iac"
    },
    "inputs": [
      {
        "name": "landscape",
        "resource": "landscape"
      },
      {
        "name": "state",
        "resource": "state"
      }
    ]
  }
]
```

</details>

##### Example cURL
```shell
curl --request GET \
    --url http://localhost:8080/api/v1/jobs \
    --header 'authorization: Bearer <token>' 
```
</details>


### List jobs in a pipeline
<details open>
    <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/jobs</b></code> <code>(lists jobs in a specific pipeline)</code></summary>

##### Headers
> | name           |  type     | data type               | description                                                           |
> |----------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                  | Bearer auth header with the access token

##### Responses
| HTTP Code | Content-Type                | Response                                                                                                   |
|-----------|-----------------------------|------------------------------------------------------------------------------------------------------------|
| `200`     | `application/json`          | See JSON example below  |
| `401`     | `application/json`          | not authorized                                                                                             |

<details>
<summary>JSON Example for 200 Response</summary>
```json
[
    {
        "id": 393,
        "name": "test-containerd-issue-iac",
        "team_name": "product-cf",
        "pipeline_id": 17,
        "pipeline_name": "test_containerd_issue_iac",
        "finished_build": {
            "id": 301596,
            "name": "10",
            "status": "aborted",
            "start_time": 1763484646,
            "end_time": 1763484663,
            "team_name": "product-cf",
            "pipeline_id": 17,
            "pipeline_name": "test_containerd_issue_iac",
            "job_name": "test-containerd-issue-iac"
        },
        "transition_build": {
            "id": 301591,
            "name": "9",
            "status": "aborted",
            "start_time": 1763484570,
            "end_time": 1763484580,
            "team_name": "product-cf",
            "pipeline_id": 17,
            "pipeline_name": "test_containerd_issue_iac",
            "job_name": "test-containerd-issue-iac"
        },
        "inputs": [
            {
                "name": "landscape",
                "resource": "landscape"
            },
            {
                "name": "state",
                "resource": "state"
            }
        ]
    }
]
```

</details>

##### Example cURL
```shell
curl --request GET \
    --url http://localhost:8080/api/v1/teams/main/pipelines/test/jobs \
    --header 'authorization: Bearer <token>' 
```
</details>
