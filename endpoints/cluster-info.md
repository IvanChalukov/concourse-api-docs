# Cluster Info

### Get current log level
<details open>
 <summary><code>GET</code> <code><b>/api/v1/log-level</b></code> <code>(retrieves the current log level)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Responses
| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:-----------------------------:|
| `200`     | text/plain; charset=utf-8 | debug/info/error/fatal |
| `401`     | text/plain; charset=utf-8 | not authorized         |

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/log-level \
  --header 'authorization: Bearer <token>'
```
</details>

---

### Set log level
<details open>
 <summary><code>PUT</code> <code><b>/api/v1/log-level</b></code> <code>(sets the current log level)</code></summary>

 ##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Body
> | name       |  type     | data type | description                                             |
> |------------|-----------|-----------|---------------------------------------------------------|
> | log level  | required  | string    | The log level to set. One of: debug, info, error, fatal |

##### Responses
| HTTP Code | Content-Type              | Response Example |
|:---------:|:-------------------------:|:----------------:|
| `200`     | None                      | None             |
| `400`     | None                      | None             |
| `401`     | text/plain; charset=utf-8 | not authorized   |

##### Example cURL
```shell
curl --request PUT \
  --url http://localhost:8080/api/v1/log-level \
  --header 'authorization: Bearer <token>'
  --header 'content-type: text/plain' \
  --data 'info'
```
</details>

---

### Download Concourse CLI binary
<details open>
 <summary><code>GET</code> <code><b>/api/v1/cli</b></code> <code>(downloads the Concourse CLI binary)</code></summary>

##### Query Parameters
> | name     |  type     | data type | description                                                         |
> |----------|-----------|-----------|---------------------------------------------------------------------|
> | platform |  required | string    | The platform for which to download the CLI - linux, darwin, windows |
> | arch     |  required | string    | The architecture for which to download the CLI - amd64, arm64       |

##### Responses
| HTTP Code | Content-Type             | Response Example |
|:---------:|:------------------------:|:----------------:|
| `200`     | application/octet-stream | CLI binary data  |
| `400`     | None                     | None             |

##### Example cURL
```shell
curl --request GET \
  --url 'http://localhost:8080/api/v1/cli?platform=linux&arch=arm64'
```
</details>

---

### Get cluster info
<details open>
 <summary><code>GET</code> <code><b>/api/v1/info</b></code> <code>(Get cluster info)</code></summary>


##### Responses
| HTTP Code | Content-Type             | Response Example       |
|:---------:|:------------------------:|:----------------------:|
| `200`     | application/json         | See JSON example below |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "version": "0.0.0-dev",
  "worker_version": "2.5",
  "feature_flags": {
    "across_step": true,
    "build_rerun": false,
    "cache_streamed_volumes": true,
    "global_resources": false,
    "pipeline_instances": true,
    "redact_secrets": false,
    "resource_causality": true
  },
  "external_url": "http://localhost:8080",
  "cluster_name": "dev"
}
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url 'http://localhost:8080/api/v1/info'
```
</details>

---

### Get credential manager info
<details open>
 <summary><code>GET</code> <code><b>/api/v1/info/creds</b></code> <code>(Get credential manager info)</code></summary>


##### Responses
| HTTP Code | Content-Type              | Response Example       |
|:---------:|:-------------------------:|:----------------------:|
| `200`     | application/json          | See JSON example below |
| `401`     | text/plain; charset=utf-8 | not authorized         |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "credhub": {
    "ca_certs": [
      "/var/vcap/jobs/web/config/env/CONCOURSE_CREDHUB_CA_CERT"
    ],
    "health": {
      "error": "not ok",
      "method": "/health"
    },
    "path_prefix": "/concourse",
    "uaa_client_id": "credhub-uaa-client",
    "url": "https://some.credhub.instance:some-port/api/"
  }
}
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url 'http://localhost:8080/api/v1/info/creds'
  --header 'authorization: Bearer <token>'
```
</details>

---