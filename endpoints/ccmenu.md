# CCMenu

### Generate CCMenu XML feed for pipelines
<details open>
 <summary><code>GET</code> <code><b>/api/v1/teams/{team_name}/cc.xml</b></code> <code>(Generates CCMenu XML feed for pipelines)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | `application/xml`  | See XML example below |

<details>
<summary>XML Example for 200 Response</summary>

```xml
<Projects>
    <Project activity="Building" lastBuildLabel="5" lastBuildStatus="Success" lastBuildTime="2025-11-21T07:17:58Z" name="test/hello-world" webUrl="http://localhost:8080/teams/main/pipelines/test/jobs/hello-world"></Project>
</Projects>
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/teams/main/cc.xml \
  --header 'authorization: Bearer <access_token>'
```
</details>

---
