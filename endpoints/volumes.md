# Volumes

### List volumes

<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/volumes</b></code> <code>(retrieves the volumes in a team)</code></summary>

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
    "id": "d312e039-b687-4b67-904d-057b289ca5dc",
    "worker_name": "e98fdeb3d200",
    "type": "resource-type",
    "container_handle": "",
    "path": "",
    "parent_handle": "",
    "resource_type": null,
    "base_resource_type": {
      "name": "time",
      "version": "dev"
    },
    "pipeline_id": 0,
    "pipeline_name": "",
    "pipeline_instance_vars": null,
    "job_name": "",
    "step_name": ""
  }
]
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/volumes \
  --header 'authorization: Bearer <access_token>'
```
</details>

---

### List destroying volumes

<details open>
 <summary><code>GET</code> <code><b>/api/v1/volumes/destroying</b></code> <code>(retrieves the volumes destroying)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Query Parameters
> | name        |  type     | data type               | description                                                           |
> |-------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | worker_name |  required | string                  | The name of the worker to list destroying volumes for                 |

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
  "8394558f-c6f1-4b56-9320-f45f32f4b4d5"
]
```
> Will be `null` if no volumes are being destroyed or no such worker exists.
</details>

```shell
curl --request GET \
  --url 'http://localhost:8080/api/v1/volumes/destroying?worker_name=e98fdeb3d200' \
  --header 'authorization: Bearer <access_token>'
```
</details>

---

### Report worker volumes
<details open>
 <summary><code>PUT</code> <code><b>/api/v1/volumes/report</b></code> <code>(Workers provide their current volumes)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |
> | Content-Type   |  required | string                   | Must be set to `application/json`                                     |

##### Query Parameters
> | name        |  type     | data type               | description                                                           |
> |-------------|-----------|-------------------------|-----------------------------------------------------------------------|
> | worker_name |  required | string                  | The name of the worker to list destroying volumes for                 |

##### Body
> | name         |  type     | data type | description                                |
> |--------------|-----------|-----------|--------------------------------------------|
> | Volumes list | required  | json      | List of volumes on worker. Example bellow  |

<details>
<summary>JSON Example for Body</summary>

```json
[
  "volume-handle-1",
  "volume-handle-2"
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
  --url 'http://localhost:8080/api/v1/volumes/report?worker_name=e98fdeb3d200' \
  --header 'authorization: Bearer <access_token>' \
  --header 'content-type: application/json' \
  --data '[
  "volume-handle-1",
  "volume-handle-2"
]'
```
</details>

---