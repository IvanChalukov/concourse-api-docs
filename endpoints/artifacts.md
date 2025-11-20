# Artifacts

### Create an artifact
<details open>
 <summary><code>POST</code> <code><b>/api/v1/teams/{team_name}/artifacts</b></code> <code>(Creates an artifact)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |
> | Content-Type   |  required | string                   | Must be set to `application/octet-stream`                             |

##### Body

> | name      |  type     | data type | description                                      |
> |-----------|-----------|-----------|--------------------------------------------------|
> | file      |  required | file      | The artifact file to be uploaded (e.g., .tar.gz) |

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `201`     | `application/json` | See JSON example below |
| `401`     | text/plain; charset=utf-8 | not authorized  |
| `500`     | text/plain; charset=utf-8 | failed to stream in to volume |

<details>
<summary>JSON Example for 201 Response</summary>

```json
{
  "id": 9,
  "name": "",
  "build_id": 0,
  "created_at": 1763556538
}
```
</details>                                       

##### Example cURL
```shell
curl --request POST \
  --url http://localhost:8080/api/v1/teams/main/artifacts \
  --header 'authorization: bearer <token>' \
  --data /path/to/artifact/artifact.tar.gz
```
</details>

---

### Get artifact details
<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/artifacts/{artifact_id}</b></code> <code>(Gets artifact details)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | application/octet-stream  | See example below |
| `401`     | text/plain; charset=utf-8 | not authorized  |
| `404`.    | application/octet-stream  | None |

<details>
<summary>Example for 200 Response</summary>

```(binary data of the artifact file)
...binary content...
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/artifacts/1 \
  --header 'authorization: bearer <token>'
```
</details>

---
