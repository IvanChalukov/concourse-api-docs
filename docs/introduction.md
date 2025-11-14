# Concourse API Documentation

Welcome to the **Concourse API** — the RESTful interface to automate, query, and manage your Concourse CI/CD pipelines.

This documentation provides a clean, Markdown-based overview of all available API endpoints, authentication methods, and data formats.  
It’s designed for developers and DevOps engineers who want to integrate Concourse into their automation workflows or external systems.

> 💡 The Concourse API powers the `fly` CLI and the Concourse web UI.  

---

## 🌐 Base URL

All requests use the following base URL: `https://<your-concourse-domain>/api/v1`
> Replace `<your-concourse-domain>` with your own Concourse installation URL.  
> Example: `https://ci.example.com/api/v1`

## 🔐 Authentication

All authenticated requests require a **Bearer Token**.
Obtain a token via token endpoint.

## 📘 API Endpoint Quick Reference

Below you’ll find categorized tables listing all primary Concourse API endpoints.  
Each table links to detailed documentation for that group.


---

### Pipeline config

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/config` | `GET` | Get pipeline configuration | [Pipeline Config](./endpoints/pipelines.md#pipeline-config) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/config` | `PUT` | Update pipeline configuration | [Pipeline Config](./endpoints/pipelines.md#pipeline-config) |

---

### 🛠️ Builds
| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/builds` | `GET` | List all builds | [Builds](./endpoints/builds.md) |
| `/api/v1/builds/:build_id` | `GET` | Get build details | [Builds](./endpoints/builds.md#build-details) |
| `/api/v1/builds/:build_id/plan` | `GET` | Get build plan | [Builds](./endpoints/builds.md#build-plan) |
| `/api/v1/builds/:build_id/events` | `GET` | Stream build events | [Builds](./endpoints/builds.md#build-events) |
| `/api/v1/builds/:build_id/resources` | `GET` | Get build resources | [Builds](./endpoints/builds.md#build-resources) |
| `/api/v1/builds/:build_id/abort` | `PUT` | Abort a build | [Builds](./endpoints/builds.md#abort-build) | 
| `/api/v1/builds/:build_id/preparation` | `GET` | Get build preparation status | [Builds](./endpoints/builds.md#build-preparation) |
| `/api/v1/builds/:build_id/artifacts` | `GET` | List build artifacts | [Builds](./endpoints/builds.md#build-artifacts) |
| `/api/v1/builds/:build_id/comment` | `PUT` | Add comment to build | [Builds](./endpoints/builds.md#build-comment) |

---

### 🔧 Jobs

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/jobs` | `GET` | List all jobs | [Jobs](./endpoints/jobs.md) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs` | `GET` | List jobs in a pipeline | [Jobs](./endpoints/jobs.md#jobs-in-pipeline) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name` | `GET` | Get job details | [Jobs](./endpoints/jobs.md#job-details) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/builds` | `GET` | List builds for a job | [Jobs](./endpoints/jobs.md#job-builds) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/builds` | `POST` | Trigger a job build | [Jobs](./endpoints/jobs.md#trigger-build) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/builds/:build_name` | `POST` | Rerun a build | [Jobs](./endpoints/jobs.md#rerun-build) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/inputs` | `GET` | Get job inputs | [Jobs](./endpoints/jobs.md#job-inputs) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/builds/:build_name` | `GET` | Get specific build for a job | [Jobs](./endpoints/jobs.md#specific-build) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/pause` | `PUT` | Pause a job | [Jobs](./endpoints/jobs.md#pause-unpause) | 
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/unpause` | `PUT` | Unpause a job | [Jobs](./endpoints/jobs.md#pause-unpause) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/schedule` | `PUT` | Enable/disable job scheduling | [Jobs](./endpoints/jobs.md#enable-disable-scheduling) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/badge` | `GET` | Get job status badge (SVG) | [Jobs](./endpoints/jobs.md#job-badge) |
| `/api/v1/pipelines/:pipeline_name/jobs/:job_name/badge` | `GET` | Get job status badge (SVG, no team) | [Jobs](./endpoints/jobs.md#job-badge) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/tasks/:step_name/cache` | `DELETE` | Clear task cache | [Jobs](./endpoints/jobs.md#clear-task-cache) |
---

### Pipelines

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/pipelines` | `GET` | List all pipelines (across teams) | [Pipelines](./endpoints/pipelines.md#list-all-pipelines) |
| `/api/v1/teams/:team_name/pipelines` | `GET` | List pipelines for a team | [Pipelines](./endpoints/pipelines.md#list-team-pipelines) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name` | `GET` | Get pipeline details | [Pipelines](./endpoints/pipelines.md#pipeline-details) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name` | `DELETE` | Delete a pipeline | [Pipelines](./endpoints/pipelines.md#delete-pipeline) |
| `/api/v1/teams/:team_name/pipelines/ordering` | `PUT` | Set pipeline ordering for a team | [Pipelines](./endpoints/pipelines.md#order-pipelines) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/ordering` | `PUT` | Set pipeline ordering within a group | [Pipelines](./endpoints/pipelines.md#order-pipelines-group) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/pause` | `PUT` | Pause a pipeline | [Pipelines](./endpoints/pipelines.md#pause-unpause) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/archive` | `PUT` | Archive a pipeline | [Pipelines](./endpoints/pipelines.md#archive) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/unpause` | `PUT` | Unpause a pipeline | [Pipelines](./endpoints/pipelines.md#pause-unpause) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/expose` | `PUT` | Expose a pipeline | [Pipelines](./endpoints/pipelines.md#expose-hide) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/hide` | `PUT` | Hide a pipeline | [Pipelines](./endpoints/pipelines.md#expose-hide) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/versions-db` | `GET` | Get pipeline versions database | [Pipelines](./endpoints/pipelines.md#versions-db) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/rename` | `PUT` | Rename a pipeline | [Pipelines](./endpoints/pipelines.md#rename) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/builds` | `GET` | List builds for a pipeline | [Pipelines](./endpoints/pipelines.md#pipeline-builds) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/builds` | `POST` | Create a build for a pipeline | [Pipelines](./endpoints/pipelines.md#create-build) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/badge` | `GET` | Get pipeline status badge (SVG) | [Pipelines](./endpoints/pipelines.md#pipeline-badge) |

---

### Resources

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/resources` | `GET` | List all resources across pipelines | [Resources](./endpoints/resources.md#list-all-resources) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources` | `GET` | List resources in a pipeline | [Resources](./endpoints/resources.md#list-resources) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/shared` | `GET` | List shared info for a resource | [Resources](./endpoints/resources.md#shared-resource) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resource-types/:resource_type_name/shared` | `GET` | List shared info for a resource type | [Resources](./endpoints/resources.md#shared-resource-type) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resource-types` | `GET` | List resource types in a pipeline | [Resources](./endpoints/resources.md#list-resource-types) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name` | `GET` | Get resource details | [Resources](./endpoints/resources.md#get-resource) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/check` | `POST` | Trigger resource check | [Resources](./endpoints/resources.md#check-resource) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/check/webhook` | `POST` | Trigger resource check via webhook | [Resources](./endpoints/resources.md#check-resource-webhook) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resource-types/:resource_type_name/check` | `POST` | Trigger resource type check | [Resources](./endpoints/resources.md#check-resource-type) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/prototypes/:prototype_name/check` | `POST` | Trigger prototype check | [Resources](./endpoints/resources.md#check-prototype) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/cache` | `DELETE` | Clear resource cache | [Resources](./endpoints/resources.md#clear-resource-cache) |

---

### Resource Versions
| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions` | `GET` | List resource versions | [Resource Versions](./endpoints/resource-versions.md#list-resource-versions) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions` | `DELETE` | Clear all resource versions | [Resource Versions](./endpoints/resource-versions.md#clear-resource-versions) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resource-types/:resource_type_name/versions` | `DELETE` | Clear all resource type versions | [Resource Versions](./endpoints/resource-versions.md#clear-resource-type-versions) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id` | `GET` | Get details for a resource version | [Resource Versions](./endpoints/resource-versions.md#get-resource-version) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/enable` | `PUT` | Enable a resource version | [Resource Versions](./endpoints/resource-versions.md#enable-disable-version) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/disable` | `PUT` | Disable a resource version | [Resource Versions](./endpoints/resource-versions.md#enable-disable-version) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/pin` | `PUT` | Pin a resource version | [Resource Versions](./endpoints/resource-versions.md#pin-unpin-version) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/unpin` | `PUT` | Unpin a resource | [Resource Versions](./endpoints/resource-versions.md#pin-unpin-version) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/pin_comment` | `PUT` | Set pin comment on resource | [Resource Versions](./endpoints/resource-versions.md#set-pin-comment) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/input_to` | `GET` | List builds with version as input | [Resource Versions](./endpoints/resource-versions.md#builds-with-version-input) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/output_of` | `GET` | List builds with version as output | [Resource Versions](./endpoints/resource-versions.md#builds-with-version-output) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/downstream` | `GET` | Get downstream resource causality | [Resource Versions](./endpoints/resource-versions.md#downstream-causality) |
| `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/upstream` | `GET` | Get upstream resource causality | [Resource Versions](./endpoints/resource-versions.md#upstream-causality) |

---

### CCMenu

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/teams/:team_name/cc.xml` | `GET` | Generate CCMenu XML feed for pipelines | [CCMenu](./endpoints/ccmenu.md) |

---

### Workers

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/workers` | `GET` | List all workers | [Workers](./endpoints/workers.md#list-workers) |
| `/api/v1/workers` | `POST` | Register a new worker | [Workers](./endpoints/workers.md#register-worker) |
| `/api/v1/workers/:worker_name/land` | `PUT` | Land a worker | [Workers](./endpoints/workers.md#land-worker) |
| `/api/v1/workers/:worker_name/retire` | `PUT` | Retire a worker | [Workers](./endpoints/workers.md#retire-worker) |
| `/api/v1/workers/:worker_name/prune` | `PUT` | Prune a worker | [Workers](./endpoints/workers.md#prune-worker) |
| `/api/v1/workers/:worker_name/heartbeat` | `PUT` | Heartbeat a worker | [Workers](./endpoints/workers.md#heartbeat-worker) |
| `/api/v1/workers/:worker_name` | `DELETE` | Delete a worker | [Workers](./endpoints/workers.md#delete-worker) |

---

### Cluster info

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/log-level` | `GET` | Get current log level | [Cluster Info](./endpoints/cluster-info.md#get-log-level) |
| `/api/v1/log-level` | `PUT` | Set log level | [Cluster Info](./endpoints/cluster-info.md#set-log-level) |
| `/api/v1/cli` | `GET` | Download Concourse CLI binary | [Cluster Info](./endpoints/cluster-info.md#download-cli) |
| `/api/v1/info` | `GET` | Get cluster info | [Cluster Info](./endpoints/cluster-info.md#get-info) |
| `/api/v1/info/creds` | `GET` | Get credential manager info | [Cluster Info](./endpoints/cluster-info.md#get-info-creds) |

---

### Users

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/user` | `GET` | Get current user info | [Users](./endpoints/users.md#get-user) |
| `/api/v1/users` | `GET` | List active users since timestamp | [Users](./endpoints/users.md#list-active-users-since) |

---

### Containers

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/containers/destroying` | `GET` | List destroying containers | [Containers](./endpoints/containers.md#list-destroying-containers) |
| `/api/v1/containers/report` | `PUT` | Report worker containers | [Containers](./endpoints/containers.md#report-worker-containers) |
| `/api/v1/teams/:team_name/containers` | `GET` | List containers for a team | [Containers](./endpoints/containers.md#list-containers) |
| `/api/v1/teams/:team_name/containers/:id` | `GET` | Get container details | [Containers](./endpoints/containers.md#get-container) |
| `/api/v1/teams/:team_name/containers/:id/hijack` | `GET` | Hijack a container | [Containers](./endpoints/containers.md#hijack-container) |

---

### Volumes

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/teams/:team_name/volumes` | `GET` | List volumes for a team | [Volumes](./endpoints/volumes.md#list-volumes) |
| `/api/v1/volumes/destroying` | `GET` | List destroying volumes | [Volumes](./endpoints/volumes.md#list-destroying-volumes) |
| `/api/v1/volumes/report` | `PUT` | Report worker volumes | [Volumes](./endpoints/volumes.md#report-worker-volumes) |

---

### Teams

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/teams` | `GET` | List all teams | [Teams](./endpoints/teams.md#list-teams) |
| `/api/v1/teams/:team_name` | `GET` | Get team details | [Teams](./endpoints/teams.md#get-team) |
| `/api/v1/teams/:team_name` | `PUT` | Set team configuration | [Teams](./endpoints/teams.md#set-team) |
| `/api/v1/teams/:team_name/rename` | `PUT` | Rename a team | [Teams](./endpoints/teams.md#rename-team) |
| `/api/v1/teams/:team_name` | `DELETE` | Delete a team | [Teams](./endpoints/teams.md#delete-team) |
| `/api/v1/teams/:team_name/builds` | `GET` | List builds for a team | [Teams](./endpoints/teams.md#list-team-builds) |
| `/api/v1/teams/:team_name/builds` | `POST` | Create a build for a team | [Teams](./endpoints/teams.md#create-team-build) |

---

### Artifacts
| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/teams/:team_name/artifacts` | `POST` | Create an artifact | [Artifacts](./endpoints/artifacts.md#create-artifact) |
| `/api/v1/teams/:team_name/artifacts/:artifact_id` | `GET` | Get artifact details | [Artifacts](./endpoints/artifacts.md#get-artifact) |

---

### Wall

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/api/v1/wall` | `GET` | Get wall message | [Wall](./endpoints/wall.md#get-wall) |
| `/api/v1/wall` | `PUT` | Set wall message | [Wall](./endpoints/wall.md#set-wall) |
| `/api/v1/wall` | `DELETE` | Clear wall message | [Wall](./endpoints/wall.md#clear-wall) |

---

### Well known

| Endpoint | Method | Description | Details |
|-----------|---------|-------------|----------|
| `/.well-known/openid-configuration` | `GET` | Get OpenID Connect configuration | [Well Known](./endpoints/well-known.md#get-openid-configuration) |
| `/.well-known/jwks.json` | `GET` | Get signing keys (JWKS) | [Well Known](./endpoints/well-known.md#get-signing-keys) |

---

> 🧭 **Tip:** Each “Details” link leads to a dedicated Markdown file with:
> - Example requests/responses  
> - Parameter tables  
> - Error codes and notes  
> - Authentication requirements  

---

**Next:** → [Authentication](./authentication.md)  
Learn how to authenticate your requests using API keys or OAuth tokens.

---

*Last updated:* **November 14, 2025**
