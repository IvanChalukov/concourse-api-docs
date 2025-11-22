# Workers

### List all workers
<details open>
<summary><code>GET</code> <code><b>/api/v1/workers</b></code> <code>(List all workers)</code></summary>

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
    "addr": "127.0.0.1:46817",
    "baggageclaim_url": "http://127.0.0.1:40131",
    "active_containers": 0,
    "active_volumes": 4,
    "active_tasks": 0,
    "resource_types": [
      {
        "type": "bosh-io-release",
        "image": "/usr/local/concourse/resource-types/bosh-io-release/rootfs.tgz",
        "version": "dev",
        "privileged": false,
        "unique_version_history": false
      },
      {
        "type": "bosh-io-stemcell",
        "image": "/usr/local/concourse/resource-types/bosh-io-stemcell/rootfs.tgz",
        "version": "dev",
        "privileged": false,
        "unique_version_history": false
      },
      {
        "type": "docker-image",
        "image": "/usr/local/concourse/resource-types/docker-image/rootfs.tgz",
        "version": "dev",
        "privileged": true,
        "unique_version_history": false
      },
      {
        "type": "git",
        "image": "/usr/local/concourse/resource-types/git/rootfs.tgz",
        "version": "dev",
        "privileged": false,
        "unique_version_history": false
      },
      {
        "type": "github-release",
        "image": "/usr/local/concourse/resource-types/github-release/rootfs.tgz",
        "version": "dev",
        "privileged": false,
        "unique_version_history": false
      },
      {
        "type": "hg",
        "image": "/usr/local/concourse/resource-types/hg/rootfs.tgz",
        "version": "dev",
        "privileged": false,
        "unique_version_history": false
      },
      {
        "type": "mock",
        "image": "/usr/local/concourse/resource-types/mock/rootfs.tgz",
        "version": "dev",
        "privileged": false,
        "unique_version_history": false
      },
      {
        "type": "pool",
        "image": "/usr/local/concourse/resource-types/pool/rootfs.tgz",
        "version": "dev",
        "privileged": false,
        "unique_version_history": false
      },
      {
        "type": "registry-image",
        "image": "/usr/local/concourse/resource-types/registry-image/rootfs.tgz",
        "version": "dev",
        "privileged": false,
        "unique_version_history": false
      },
      {
        "type": "s3",
        "image": "/usr/local/concourse/resource-types/s3/rootfs.tgz",
        "version": "dev",
        "privileged": false,
        "unique_version_history": false
      },
      {
        "type": "semver",
        "image": "/usr/local/concourse/resource-types/semver/rootfs.tgz",
        "version": "dev",
        "privileged": false,
        "unique_version_history": false
      },
      {
        "type": "time",
        "image": "/usr/local/concourse/resource-types/time/rootfs.tgz",
        "version": "dev",
        "privileged": false,
        "unique_version_history": true
      }
    ],
    "platform": "linux",
    "tags": null,
    "team": "",
    "name": "e98fdeb3d200",
    "version": "2.5",
    "start_time": 1763545517,
    "ephemeral": false,
    "state": "running"
  }
]
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/workers \
  --header 'authorization: Bearer <token>'
```
</details>

---

### Register a new worker
<details open>
<summary><code>POST</code> <code><b>/api/v1/workers</b></code> <code>(Register a new worker)</code></summary>

> #### Note: This endpoint is restricted to system-level access and is typically called automatically by worker processes through TSA authentication.Direct API access requires SSH key-based authentication through the TSA gateway.

</details>

---

### Land a worker
<details open>
<summary><code>PUT</code> <code><b>/api/v1/workers/{worker_name}/land</b></code> <code>(Land a worker)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | None               | None                   |
| `401`     | text/plain; charset=utf-8 | not authorized  |
| `500`     | None               | None                   |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/workers/e98fdeb3d200/land \
  --header 'authorization: Bearer <token>'
```
</details>

---

### Retire a worker
<details open>
<summary><code>PUT</code> <code><b>/api/v1/workers/{worker_name}/retire</b></code> <code>(Retire a worker)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | None               | None                   |
| `401`     | text/plain; charset=utf-8 | not authorized  |
| `500`     | None               | None                   |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/workers/e98fdeb3d200/retire \
  --header 'authorization: Bearer <token>'
```
</details>

---

### Prune a worker
<details open>
<summary><code>PUT</code> <code><b>/api/v1/workers/{worker_name}/prune</b></code> <code>(Prune a worker)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Responses

| HTTP Code | Content-Type              | Response Example                          |
|:---------:|:-------------------------:|:-----------------------------------------:|
| `200`     | None                      | None                                      |
| `400`     | application/json          | {"stderr": "cannot prune running worker"} |
| `401`     | text/plain; charset=utf-8 | not authorized                            |
| `500`     | None                      | None                                      |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/workers/e98fdeb3d200/prune \
  --header 'authorization: Bearer <token>'
```
</details>

---

### Heartbeat a worker
<details open>
<summary><code>PUT</code> <code><b>/api/v1/workers/{worker_name}/heartbeat</b></code> <code>(Heartbeat a worker)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Query Parameters
> | name        |  type     | data type               | description                                                           |
> |-------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | ttl         |  optional | string                  | Time-to-live duration (e.g., 30s, 5m, 1h)                             |

##### Body
Could be an empty JSON object `{}`.

##### Responses

| HTTP Code | Content-Type              | Response Example       |
|:---------:|:-------------------------:|:----------------------:|
| `200`     | application/json          | See JSON example below |
| `401`     | text/plain; charset=utf-8 | not authorized         |
| `500`     | None                      | None                   |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "addr": "127.0.0.1:42785",
  "baggageclaim_url": "http://127.0.0.1:37799",
  "active_containers": 0,
  "active_volumes": 0,
  "active_tasks": 0,
  "resource_types": [
    {
      "type": "bosh-io-release",
      "image": "/usr/local/concourse/resource-types/bosh-io-release/rootfs.tgz",
      "version": "dev",
      "privileged": false,
      "unique_version_history": false
    },
    {
      "type": "bosh-io-stemcell",
      "image": "/usr/local/concourse/resource-types/bosh-io-stemcell/rootfs.tgz",
      "version": "dev",
      "privileged": false,
      "unique_version_history": false
    },
    {
      "type": "docker-image",
      "image": "/usr/local/concourse/resource-types/docker-image/rootfs.tgz",
      "version": "dev",
      "privileged": true,
      "unique_version_history": false
    },
    {
      "type": "git",
      "image": "/usr/local/concourse/resource-types/git/rootfs.tgz",
      "version": "dev",
      "privileged": false,
      "unique_version_history": false
    },
    {
      "type": "github-release",
      "image": "/usr/local/concourse/resource-types/github-release/rootfs.tgz",
      "version": "dev",
      "privileged": false,
      "unique_version_history": false
    },
    {
      "type": "hg",
      "image": "/usr/local/concourse/resource-types/hg/rootfs.tgz",
      "version": "dev",
      "privileged": false,
      "unique_version_history": false
    },
    {
      "type": "mock",
      "image": "/usr/local/concourse/resource-types/mock/rootfs.tgz",
      "version": "dev",
      "privileged": false,
      "unique_version_history": false
    },
    {
      "type": "pool",
      "image": "/usr/local/concourse/resource-types/pool/rootfs.tgz",
      "version": "dev",
      "privileged": false,
      "unique_version_history": false
    },
    {
      "type": "registry-image",
      "image": "/usr/local/concourse/resource-types/registry-image/rootfs.tgz",
      "version": "dev",
      "privileged": false,
      "unique_version_history": false
    },
    {
      "type": "s3",
      "image": "/usr/local/concourse/resource-types/s3/rootfs.tgz",
      "version": "dev",
      "privileged": false,
      "unique_version_history": false
    },
    {
      "type": "semver",
      "image": "/usr/local/concourse/resource-types/semver/rootfs.tgz",
      "version": "dev",
      "privileged": false,
      "unique_version_history": false
    },
    {
      "type": "time",
      "image": "/usr/local/concourse/resource-types/time/rootfs.tgz",
      "version": "dev",
      "privileged": false,
      "unique_version_history": true
    }
  ],
  "platform": "linux",
  "tags": null,
  "team": "",
  "name": "99d24f8ad9cf",
  "version": "2.5",
  "start_time": 1763652167,
  "ephemeral": false,
  "state": "running"
}
```
</details>

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/workers/99d24f8ad9cf/heartbeat \
  --header 'authorization: Bearer <token>' \
  --header 'content-type: application/json' \
  --data '{}'
```
</details>

---

### Delete a worker
<details open>
<summary><code>DELETE</code> <code><b>/api/v1/workers/{worker_name}</b></code> <code>(Delete a worker)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:-------------------------:|:---------------:|
| `200`     | None                      | None            |
| `401`     | text/plain; charset=utf-8 | not authorized  |
| `500`     | None                      | None            |

##### Example cURL
```shell
curl --request DELETE \
  --url http://localhost:8080/api/v1/workers/e98fdeb3d200 \
  --header 'authorization: Bearer <token>'
```
</details>

---