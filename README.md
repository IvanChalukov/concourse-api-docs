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


### Login/Logout
| Description                  | Method | Endpoint                      |
|------------------------------|--------|-------------------------------|
| [Login](./endpoints/authentication.md#login)   | `POST` | `/sky/issuer/token`         |
| [Logout](./endpoints/authentication.md#logout) | `GET` | `/sky/logout`               | 
---

### Pipeline config

| Description                   | Method | Endpoint                                                         |
|-------------------------------|--------|------------------------------------------------------------------|
| [Get pipeline configuration](./endpoints/pipelines.md#get-pipeline-configuration)    | `GET`  | `/api/v1/teams/:team_name/pipelines/:pipeline_name/config`        |
| [Create/Update pipeline configuration](./endpoints/pipelines.md#createupdate-pipeline-configuration) | `PUT`  | `/api/v1/teams/:team_name/pipelines/:pipeline_name/config`        |

---

### Builds

| Description                      | Method | Endpoint                                      |
|----------------------------------|--------|-----------------------------------------------|
| [List all builds](./endpoints/builds.md#list-builds) | `GET`  | `/api/v1/builds`                              |
| [Get build details](./endpoints/builds.md#get-build-details) | `GET`  | `/api/v1/builds/:build_id`                    |
| [Get build plan](./endpoints/builds.md#get-build-plan) | `GET`  | `/api/v1/builds/:build_id/plan`               |
| [Stream build events](./endpoints/builds.md#stream-build-events) | `GET`  | `/api/v1/builds/:build_id/events`             |
| [Get build resources](./endpoints/builds.md#get-build-resources) | `GET`  | `/api/v1/builds/:build_id/resources`          |
| [Abort a build](./endpoints/builds.md#abort-build) | `PUT`  | `/api/v1/builds/:build_id/abort`              |
| [Get build preparation status](./endpoints/builds.md#get-build-preparation-status) | `GET`  | `/api/v1/builds/:build_id/preparation`        |
| [List build artifacts](./endpoints/builds.md#get-build-artifacts) | `GET`  | `/api/v1/builds/:build_id/artifacts`          |
| [Add comment to build](./endpoints/builds.md#add-comment-to-build) | `PUT`  | `/api/v1/builds/:build_id/comment`            |

---

### Jobs

| Description                                   | Method | Endpoint                                      |
|-----------------------------------------------|--------|-----------------------------------------------|
| [List all jobs](./endpoints/jobs.md#list-all-jobs) | `GET` | `/api/v1/jobs` |
| [List jobs in a pipeline](./endpoints/jobs.md#list-jobs-in-a-pipeline) | `GET` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs` |
| [Get job details](./endpoints/jobs.md#get-job-details) | `GET` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name` |
| [List builds for a job](./endpoints/jobs.md#list-builds-for-a-job) | `GET` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/builds` |
| [Trigger a job build](./endpoints/jobs.md#trigger-a-job-build) | `POST` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/builds` |
| [Rerun a build](./endpoints/jobs.md#rerun-a-build) | `POST` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/builds/:build_name` |
| [Get job inputs](./endpoints/jobs.md#get-job-inputs) | `GET` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/inputs` |
| [Get specific build for a job](./endpoints/jobs.md#get-specific-build-for-a-job) | `GET` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/builds/:build_name` |
| [Pause a job](./endpoints/jobs.md#pause-a-job) | `PUT` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/pause` |
| [Unpause a job](./endpoints/jobs.md#unpause-a-job) | `PUT` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/unpause` |
| [Trigger scheduling for job](./endpoints/jobs.md#trigger-scheduling-for-job) | `PUT` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/schedule` |
| [Get job status badge (SVG)](./endpoints/jobs.md#get-job-status-badge) | `GET` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/badge` |
| [Get job status badge (SVG, main team)](./endpoints/jobs.md#get-job-status-badge-main-team) | `GET` | `/api/v1/pipelines/:pipeline_name/jobs/:job_name/badge` |
| [Clear task cache](./endpoints/jobs.md#clear-task-cache) | `DELETE` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/jobs/:job_name/tasks/:step_name/cache` |
---

### Pipelines

| Description | Method | Endpoint |
|-------------|--------|----------|
| [List all pipelines (across teams)](./endpoints/pipelines.md#list-all-pipelines) | `GET` | `/api/v1/pipelines` |
| [List pipelines for a team](./endpoints/pipelines.md#list-pipelines-for-team) | `GET` | `/api/v1/teams/:team_name/pipelines` |
| [Get pipeline details](./endpoints/pipelines.md#get-pipeline-details) | `GET` | `/api/v1/teams/:team_name/pipelines/:pipeline_name` |
| [Delete a pipeline](./endpoints/pipelines.md#delete-a-pipeline) | `DELETE` | `/api/v1/teams/:team_name/pipelines/:pipeline_name` |
| [Set pipeline ordering for a team](./endpoints/pipelines.md#set-pipeline-ordering-for-a-team) | `PUT` | `/api/v1/teams/:team_name/pipelines/ordering` |
| [Set pipeline ordering within a group](./endpoints/pipelines.md#set-pipeline-ordering-within-a-group) | `PUT` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/ordering` |
| [Pause a pipeline](./endpoints/pipelines.md#pause-a-pipeline) | `PUT` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/pause` |
| [Archive a pipeline](./endpoints/pipelines.md#archive-a-pipeline) | `PUT` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/archive` |
| [Unpause a pipeline](./endpoints/pipelines.md#unpause-a-pipeline) | `PUT` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/unpause` |
| [Expose a pipeline](./endpoints/pipelines.md#expose-a-pipeline) | `PUT` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/expose` |
| [Hide a pipeline](./endpoints/pipelines.md#hide-a-pipeline) | `PUT` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/hide` |
| [Get pipeline versions database](./endpoints/pipelines.md#get-pipeline-versions-database) | `GET` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/versions-db` |
| [Rename a pipeline](./endpoints/pipelines.md#rename-a-pipeline) | `PUT` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/rename` |
| [List builds for a pipeline](./endpoints/pipelines.md#list-builds-for-a-pipeline) | `GET` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/builds` |
| [Create a build for a pipeline](./endpoints/pipelines.md#create-a-build-for-a-pipeline) | `POST` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/builds` |
| [Get pipeline status badge (SVG)](./endpoints/pipelines.md#get-pipeline-status-badge-svg) | `GET` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/badge` |

---

### Resources

| Description                                                      | Method   | Endpoint                                                                 |
|------------------------------------------------------------------|----------|-------------------------------------------------------------------------|
| [List all resources across pipelines](./endpoints/resources.md#list-all-resources) | `GET`    | `/api/v1/resources`                                                      |
| [List resources in a pipeline](./endpoints/resources.md#list-resources-in-a-pipeline)           | `GET`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources`            |
| [List shared info for a resource](./endpoints/resources.md#list-shared-info-for-a-resource)       | `GET`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/shared` |
| [List shared info for a resource type](./endpoints/resources.md#list-shared-info-for-a-resource-type) | `GET`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resource-types/:resource_type_name/shared` |
| [List resource types in a pipeline](./endpoints/resources.md#list-resource-types) | `GET`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resource-types`       |
| [Get resource details](./endpoints/resources.md#get-resource)                     | `GET`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name` |
| [Trigger resource check](./endpoints/resources.md#check-resource)                 | `POST`   | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/check` |
| [Trigger resource check via webhook](./endpoints/resources.md#check-resource-webhook) | `POST`   | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/check/webhook` |
| [Trigger resource type check](./endpoints/resources.md#check-resource-type)       | `POST`   | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resource-types/:resource_type_name/check` |
| [Trigger prototype check](./endpoints/resources.md#check-prototype)               | `POST`   | `/api/v1/teams/:team_name/pipelines/:pipeline_name/prototypes/:prototype_name/check` |
| [Clear resource cache](./endpoints/resources.md#clear-resource-cache)             | `DELETE` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/cache` |

---

### Resource Versions
| Description                                                                                                 | Method   | Endpoint                                                                                                         |
|-------------------------------------------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------------------------------|
| [List resource versions](./endpoints/resource-versions.md#list-resource-versions)                           | `GET`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions`                            |
| [Clear all resource versions](./endpoints/resource-versions.md#clear-resource-versions)                     | `DELETE` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions`                            |
| [Clear all resource type versions](./endpoints/resource-versions.md#clear-resource-type-versions)           | `DELETE` | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resource-types/:resource_type_name/versions`                  |
| [Get details for a resource version](./endpoints/resource-versions.md#get-resource-version-details)          | `GET`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id` |
| [Enable a resource version](./endpoints/resource-versions.md#enable-resource-version)                       | `PUT`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/enable` |
| [Disable a resource version](./endpoints/resource-versions.md#disable-resource-version)                     | `PUT`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/disable` |
| [Pin a resource version](./endpoints/resource-versions.md#pin-resource-version)                             | `PUT`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/pin` |
| [Unpin a resource](./endpoints/resource-versions.md#unpin-resource)                                         | `PUT`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/unpin`                               |
| [Set pin comment on resource](./endpoints/resource-versions.md#set-pin-comment)                             | `PUT`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/pin_comment`                         |
| [List builds with version as input](./endpoints/resource-versions.md#list-builds-with-version-as-input)     | `GET`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/input_to` |
| [List builds with version as output](./endpoints/resource-versions.md#list-builds-with-version-as-output)   | `GET`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/output_of` |
| [Get downstream resource causality](./endpoints/resource-versions.md#get-downstream-causality)              | `GET`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/downstream` |
| [Get upstream resource causality](./endpoints/resource-versions.md#get-upstream-causality)                  | `GET`    | `/api/v1/teams/:team_name/pipelines/:pipeline_name/resources/:resource_name/versions/:resource_config_version_id/upstream`   |

### CCMenu

| Description | Method | Endpoint |
|-------------|--------|----------|
| [Generate CCMenu XML feed for pipelines](./endpoints/ccmenu.md) | `GET` | `/api/v1/teams/:team_name/cc.xml` |

---

### Workers

| Description                                   | Method | Endpoint                                      |
|-----------------------------------------------|--------|-----------------------------------------------|
| [List all workers](./endpoints/workers.md#list-workers)           | `GET`  | `/api/v1/workers`                             |
| [Register a new worker](./endpoints/workers.md#register-worker)   | `POST` | `/api/v1/workers`                             |
| [Land a worker](./endpoints/workers.md#land-worker)               | `PUT`  | `/api/v1/workers/:worker_name/land`           |
| [Retire a worker](./endpoints/workers.md#retire-worker)           | `PUT`  | `/api/v1/workers/:worker_name/retire`         |
| [Prune a worker](./endpoints/workers.md#prune-worker)             | `PUT`  | `/api/v1/workers/:worker_name/prune`          |
| [Heartbeat a worker](./endpoints/workers.md#heartbeat-worker)     | `PUT`  | `/api/v1/workers/:worker_name/heartbeat`      |
| [Delete a worker](./endpoints/workers.md#delete-worker)           | `DELETE` | `/api/v1/workers/:worker_name`               |

---

### Cluster info

| Description                                   | Method | Endpoint                   |
|-----------------------------------------------|--------|----------------------------|
| [Get current log level](./endpoints/cluster-info.md#get-log-level)         | `GET`  | `/api/v1/log-level`         |
| [Set log level](./endpoints/cluster-info.md#set-log-level)                 | `PUT`  | `/api/v1/log-level`         |
| [Download Concourse CLI binary](./endpoints/cluster-info.md#download-cli)  | `GET`  | `/api/v1/cli`               |
| [Get cluster info](./endpoints/cluster-info.md#get-info)                   | `GET`  | `/api/v1/info`              |
| [Get credential manager info](./endpoints/cluster-info.md#get-info-creds)  | `GET`  | `/api/v1/info/creds`        |

---

### Users

| Description | Method | Endpoint |
|-------------|--------|----------|
| [Get current user info](./endpoints/users.md#get-user) | `GET` | `/api/v1/user` |
| [List active users since timestamp](./endpoints/users.md#list-active-users-since) | `GET` | `/api/v1/users` |

---

### Containers

| Description | Method | Endpoint |
|-------------|--------|----------|
| [List containers for a team](./endpoints/containers.md#list-containers-for-a-team) | `GET` | `/api/v1/teams/:team_name/containers` |
| [Get container details](./endpoints/containers.md#get-container-details) | `GET` | `/api/v1/teams/:team_name/containers/:id` |
| [Hijack a container](./endpoints/containers.md#hijack-a-container) | `GET` | `/api/v1/teams/:team_name/containers/:id/hijack` |
| [List destroying containers](./endpoints/containers.md#list-destroying-containers) | `GET` | `/api/v1/containers/destroying` |
| [Report worker containers](./endpoints/containers.md#report-worker-containers) | `PUT` | `/api/v1/containers/report` |

---

### Volumes

| Description | Method | Endpoint |
|-------------|--------|----------|
| [List volumes](./endpoints/volumes.md#list-volumes) | `GET` | `/api/v1/teams/:team_name/volumes` |
| [List destroying volumes](./endpoints/volumes.md#list-destroying-volumes) | `GET` | `/api/v1/volumes/destroying` |
| [Report worker volumes](./endpoints/volumes.md#report-worker-volumes) | `PUT` | `/api/v1/volumes/report` |

---

### Teams

| Description | Method | Endpoint |
|-------------|--------|----------|
| [List all teams](./endpoints/teams.md#list-all-teams) | `GET` | `/api/v1/teams` |
| [Get team details](./endpoints/teams.md#get-team-details) | `GET` | `/api/v1/teams/:team_name` |
| [Set team configuration](./endpoints/teams.md#set-team-configuration) | `PUT` | `/api/v1/teams/:team_name` |
| [Rename a team](./endpoints/teams.md#rename-a-team) | `PUT` | `/api/v1/teams/:team_name/rename` |
| [Delete a team](./endpoints/teams.md#delete-a-team) | `DELETE` | `/api/v1/teams/:team_name` |
| [List builds for a team](./endpoints/teams.md#list-builds-for-a-team) | `GET` | `/api/v1/teams/:team_name/builds` |
| [Create a build for a team](./endpoints/teams.md#create-a-build-for-a-team) | `POST` | `/api/v1/teams/:team_name/builds` |

---

### Artifacts
| Description            | Method | Endpoint                                               |
|------------------------|--------|--------------------------------------------------------|
| [Create an artifact](./endpoints/artifacts.md#create-an-artifact) | `POST` | `/api/v1/teams/:team_name/artifacts`                  |
| [Get artifact details](./endpoints/artifacts.md#get-artifact-details)  | `GET`  | `/api/v1/teams/:team_name/artifacts/:artifact_id`     |

---

### Wall

| Description | Method | Endpoint |
|-------------|--------|----------|
| [Get wall message](./endpoints/wall.md#get-wall-message) | `GET` | `/api/v1/wall` |
| [Set wall message](./endpoints/wall.md#set-wall-message) | `PUT` | `/api/v1/wall` |
| [Clear wall message](./endpoints/wall.md#clear-wall-message) | `DELETE` | `/api/v1/wall` |

---

### Well known

| Description | Method | Endpoint |
|-------------|--------|----------|
| [Get OpenID Connect configuration](./endpoints/well-known.md#get-openid-connect-configuration) | `GET` | `/.well-known/openid-configuration` |
| [Get signing keys (JWKS)](./endpoints/well-known.md#get-json-web-key-set) | `GET` | `/.well-known/jwks.json` |

---

> 🧭 **Tip:** Each “Details” link leads to a dedicated Markdown file with:
> - Example requests/responses  
> - Parameter tables  
> - Error codes and notes  
> - Authentication requirements  

---