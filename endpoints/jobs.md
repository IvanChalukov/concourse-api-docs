# Jobs

### List all jobs
<details open>
    <summary><code>GET</code> <code><b>/api/v1/jobs</b></code> <code>(lists all jobs)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|------------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response                   |
|-----------|---------------------------|----------------------------|
| `200`     | `application/json`        | See JSON example below     |
| `401`     | text/plain; charset=utf-8 | not authorized             |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "id": 393,
    "name": "test-containerd-issue-iac",
    "team_name": "main",
    "pipeline_id": 17,
    "pipeline_name": "test_containerd_issue_iac",
    "finished_build": {
      "id": 301596,
      "name": "10",
      "status": "aborted",
      "start_time": 1763484646,
      "end_time": 1763484663,
      "team_name": "main",
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
      "team_name": "main",
      "pipeline_id": 17,
      "pipeline_name": "test_containerd_issue_iac",
      "job_name": "test-containerd-issue-iac"
    },
    "inputs": [
      {
        "name": "l",
        "resource": "l"
      },
      {
        "name": "s",
        "resource": "s"
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

| name          | type     | data type | description                              |
|---------------|----------|-----------|------------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response               |
|-----------|---------------------------|------------------------|
| `200`     | `application/json`        | See JSON example below |
| `401`     | text/plain; charset=utf-8 | not authorized         |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
    {
        "id": 393,
        "name": "test-containerd-issue-iac",
        "team_name": "main",
        "pipeline_id": 17,
        "pipeline_name": "test_containerd_issue_iac",
        "finished_build": {
            "id": 301596,
            "name": "10",
            "status": "aborted",
            "start_time": 1763484646,
            "end_time": 1763484663,
            "team_name": "main",
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
            "team_name": "main",
            "pipeline_id": 17,
            "pipeline_name": "test_containerd_issue_iac",
            "job_name": "test-containerd-issue-iac"
        },
        "inputs": [
            {
                "name": "l",
                "resource": "l"
            },
            {
                "name": "s",
                "resource": "s"
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

### Get job details
<details open>
    <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/jobs/{job_name}</b></code> <code>(retrieves details of a specific job in a pipeline)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|------------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response               |
|-----------|---------------------------|------------------------|
| `200`     | `application/json`        | See JSON example below |
| `401`     | text/plain; charset=utf-8 | not authorized         |
| `404`     | text/plain; charset=utf-8 | job not found          |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
    "id": 393,
    "name": "test-containerd-issue-iac",
    "team_name": "main",
    "pipeline_id": 17,
    "pipeline_name": "test_containerd_issue_iac",
    "next_build": null,
    "finished_build": {
        "id": 301596,
        "team_name": "main",
        "name": "10",
        "status": "aborted",
        "api_url": "/api/v1/builds/301596",
        "comment": "test-api",
        "job_name": "test-containerd-issue-iac",
        "pipeline_id": 17,
        "pipeline_name": "test_containerd_issue_iac",
        "start_time": 1763484646,
        "end_time": 1763484663,
        "created_by": "test"
    },    
    "inputs": [
        {
        "name": "s",
        "resource": "s",
        "trigger": false
        },
        {
        "name": "a",
        "resource": "a",
        "trigger": false
        }
    ]
}
```
</details>

##### Example cURL

```shell
curl --request GET \
    --url http://localhost:8080/api/v1/teams/main/pipelines/test/jobs/test-job \
    --header 'authorization: Bearer <token>'
```

</details>

---

### List builds for a job
<details open>
    <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/jobs/{job_name}/builds</b></code> <code>(lists builds for a specific job)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|------------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |


##### Query Parameters

| name       | type     | data type | description                                                                         |
|------------|----------|-----------|-------------------------------------------------------------------------------------|
| limit      | optional | integer   | Maximum number of builds to return (default: 100)                                   |
| from       | optional | integer   | Return builds with ID less than this value (for pagination)                         |
| to         | optional | integer   | Return builds with ID greater than this value (for pagination)                      |
| timestamps | optional | boolean   | If true, `from` and `to` are treated as timestamps instead of IDs (default: false) |

##### Responses

| HTTP Code | Content-Type              | Response               |
|-----------|---------------------------|------------------------|
| `200`     | `application/json`        | See JSON example below |
| `401`     | text/plain; charset=utf-8 | not authorized         |
| `404`     | text/plain; charset=utf-8 | None                   |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
    {
         "id": 301596,
        "team_name": "main",
        "name": "10",
        "status": "aborted",
        "api_url": "/api/v1/builds/301596",
        "comment": "test-api",
        "job_name": "test-containerd-issue-",
        "pipeline_id": 17,
        "pipeline_name": "test_containerd_issue_",
        "start_time": 1763484646,
        "end_time": 1763484663,
        "created_by": "test"
    },
    {
        "id": 301591,
        "team_name": "main",
        "name": "9",
        "status": "aborted",
        "api_url": "/api/v1/builds/301591",
        "job_name": "test-containerd-issue-iac",
        "pipeline_id": 17,
        "pipeline_name": "test_containerd_issue_",
        "start_time": 1763484570,
        "end_time": 1763484580,
        "created_by": "test"
    }
]
```

</details>

##### Example cURL

```shell
curl --request GET \
    --url http://localhost:8080/api/v1/teams/main/pipelines/test/jobs/test-job/builds \
    --header 'authorization: Bearer <token>'
```

</details>

---

### Trigger a job build
<details open>
    <summary><code>POST</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/jobs/{job_name}/builds</b></code> <code>(triggers a new build for a specific job)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|--------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response                   |
|-----------|---------------------------|----------------------------|
| `200`     | `application/json`        | See JSON example below     |
| `401`     | text/plain; charset=utf-8 | not authorized             |
| `404`     | text/plain; charset=utf-8 | None                       |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
    "id": 303193,
    "team_name": "main",
    "name": "11",
    "status": "pending",
    "api_url": "/api/v1/builds/303193",
    "job_name": "test-containerd-issue-iac",
    "pipeline_id": 17,
    "pipeline_name": "test_containerd_issue_iac",
    "created_by": "test"
}
```

</details>

##### Example cURL

```shell
curl --request POST \
    --url http://localhost:8080/api/v1/teams/main/pipelines/test/jobs/test-job/builds \
    --header 'authorization: Bearer <token>'
```

</details>

---

### Rerun a build
<details open>
    <summary><code>POST</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/jobs/{job_name}/builds/{build_id}</b></code> <code>(reruns a specific build for a job)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|--------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response                   |
|-----------|---------------------------|----------------------------|
| `200`     | `application/json`        | See JSON example below     |
| `401`     | text/plain; charset=utf-8 | not authorized             |
| `404`     | text/plain; charset=utf-8 | None                       |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
    "id": 303194,
    "team_name": "main",
    "name": "12",
    "status": "pending",
    "api_url": "/api/v1/builds/303194",
    "job_name": "test-containerd-issue-iac",
    "pipeline_id": 17,
    "pipeline_name": "test_containerd_issue_iac",
    "created_by": "test"
}
```

</details>

##### Example cURL

```shell
curl --request POST \
    --url http://localhost:8080/api/v1/teams/main/pipelines/test/jobs/test-job/builds/303193 \
    --header 'authorization: Bearer <token>'
```

</details>

---

### Get job inputs

<details open>
    <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/jobs/{job_name}/inputs</b></code> <code>(retrieves the inputs for a specific job)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|--------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response                   |
|-----------|---------------------------|----------------------------|
| `200`     | `application/json`        | See JSON example below     |
| `401`     | text/plain; charset=utf-8 | not authorized             |
| `404`     | text/plain; charset=utf-8 | None                       |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "name": "s",
    "resource": "s",
    "type": "git",
    "source": {
      "branch": "s",
      "password": "((password))",
      "skip_ssl_verification": false,
      "uri": "((repository))",
      "username": "((user))"
    },
    "version": {
      "ref": "7e3dc6ba2f3c8a0d824b4e87f0dba73c39b33266"
    }
  },
  {
    "name": "l",
    "resource": "l",
    "type": "git",
    "source": {
      "branch": "containerd-issue",
      "ignore_paths": [
        "state/*",
        "deployments/concourse/onboarding/*",
        "deployments/global-failover/*"
      ],
      "password": "((password))",
      "skip_ssl_verification": false,
      "submodule_credentials": [
        {
          "host": "github.com",
          "password": "((technical-serviceuser))",
          "username": "serviceuser"
        }
      ],
      "uri": "((repository))",
      "username": "((user))",
      "version_depth": 50
    },
    "version": {
      "ref": "f4fd419c9634d8afa13830d41a1a34f07fd3717b"
    }
  }
]
```

</details>

##### Example cURL

```shell
curl --request GET \
    --url http://localhost:8080/api/v1/teams/main/pipelines/test/jobs/test-job/inputs \
    --header 'authorization: Bearer <token>'
```

</details>

---

### Get specific build for a job

<details open>
    <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/jobs/{job_name}/builds/{build_id}</b></code> <code>(retrieves details of a specific build for a job)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|--------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response                   |
|-----------|---------------------------|----------------------------|
| `200`     | `application/json`        | See JSON example below     |
| `401`     | text/plain; charset=utf-8 | not authorized             |
| `404`     | text/plain; charset=utf-8 | None                       |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "id": 206380,
  "team_name": "main",
  "name": "6",
  "status": "succeeded",
  "api_url": "/api/v1/builds/206380",
  "job_name": "test-containerd-issue-iac",
  "pipeline_id": 17,
  "pipeline_name": "test_containerd_issue_iac",
  "start_time": 1762158266,
  "end_time": 1762158321,
  "created_by": "test"
}
```

</details>

##### Example cURL

```shell
curl --request GET \
    --url http://localhost:8080/api/v1/teams/main/pipelines/test/jobs/test-job/builds/301596 \
    --header 'authorization: Bearer <token>'
```

</details>

---

### Pause a job

<details open>
    <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/jobs/{job_name}/pause</b></code> <code>(pauses a specific job)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|--------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response       |
|-----------|---------------------------|----------------|
| `200`     | `application/json`        | None           |
| `401`     | text/plain; charset=utf-8 | not authorized |
| `404`     | text/plain; charset=utf-8 | None           |

##### Example cURL

```shell
curl --request PUT \
    --url http://localhost:8080/api/v1/teams/main/pipelines/test/jobs/test-job/pause \
    --header 'authorization: Bearer <token>'
```

</details>

---

### Unpause a job
<details open>
    <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/jobs/{job_name}/unpause</b></code> <code>(unpauses a specific job)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|--------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response       |
|-----------|---------------------------|----------------|
| `200`     | `application/json`        | None           |
| `401`     | text/plain; charset=utf-8 | not authorized |
| `404`     | text/plain; charset=utf-8 | None           |

##### Example cURL

```shell
curl --request PUT \
    --url http://localhost:8080/api/v1/teams/main/pipelines/test/jobs/test-job/unpause \
    --header 'authorization: Bearer <token>'
```

</details>

---

### Trigger scheduling for job

<details open>
    <summary><code>PUT</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/jobs/{job_name}/schedule</b></code> <code>(enables or disables scheduling for a specific job)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|--------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response       |
|-----------|---------------------------|----------------|
| `200`     | `application/json`        | None           |
| `401`     | text/plain; charset=utf-8 | not authorized |
| `404`     | text/plain; charset=utf-8 | None           |

##### Example cURL

```shell
curl --request PUT \
    --url http://localhost:8080/api/v1/teams/main/pipelines/test/jobs/test-job/schedule \
    --header 'authorization: Bearer <token>'
```

</details>

---

### Get job status badge
<details open>
    <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/jobs/{job_name}/badge</b></code> <code>(retrieves the status badge for a specific job)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|--------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response                                |
|-----------|---------------------------|-----------------------------------------|
| `200`     | `image/svg+xml`           | SVG badge representing the job status   |
| `401`     | text/plain; charset=utf-8 | not authorized                          |
| `404`     | text/plain; charset=utf-8 | None                                    |

##### Example cURL

```shell
curl --request GET \
    --url http://localhost:8080/api/v1/teams/main/pipelines/test/jobs/test-job/badge \
    --header 'authorization: Bearer <token>'
```

</details>

---

### Get job status badge main team

<details open>
    <summary><code>GET</code> <code><b>/api/v1/pipelines/{pipeline_name}/jobs/{job_name}/badge</b></code> <code>(retrieves the status badge for a specific job from the main team)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|--------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response                                |
|-----------|---------------------------|-----------------------------------------|
| `200`     | `image/svg+xml`           | SVG badge representing the job status   |
| `401`     | text/plain; charset=utf-8 | not authorized                          |
| `404`     | text/plain; charset=utf-8 | None                                    |

##### Example cURL

```shell
curl --request GET \
    --url http://localhost:8080/api/v1/pipelines/test/jobs/test-job/badge \
    --header 'authorization: Bearer <token>'
```

</details>

---

### Clear task cache

<details open>
    <summary><code>DELETE</code> <code><b>/api/v1/teams/{team_name}/pipelines/{pipeline_name}/jobs/{job_name}/tasks/{step_name}/cache</b></code> <code>(clears a specific task cache for a job)</code></summary>

##### Headers

| name          | type     | data type | description                              |
|---------------|----------|-----------|--------------------------------------|
| Authorization | required | string    | Bearer auth header with the access token |

##### Responses

| HTTP Code | Content-Type              | Response                |
|-----------|---------------------------|-------------------------|
| `200`     | application/json          | { "caches_removed":0 }  |
| `401`     | text/plain; charset=utf-8 | not authorized          |
| `404`     | text/plain; charset=utf-8 | None                    |

##### Example cURL

```shell
curl --request DELETE \
    --url http://localhost:8080/api/v1/teams/main/pipelines/test/jobs/test-job/tasks/test-step/cache \
    --header 'authorization: Bearer <token>'
```

</details>