# Review `kubectl-ai`

Review of the [`kubectl-ai`](https://github.com/sozercan/kubectl-ai) plugin for creating and publishing Kubernetes manifests using OpenAI GPT.

## Installation

Add to `krew` index and install with:

```bash
kubectl krew index add kubectl-ai https://github.com/sozercan/kubectl-ai
kubectl krew install kubectl-ai/kubectl-ai
```

## Usage

`kubectl-ai` requires a valid Kubernetes configuration and [OpenAI API key](https://platform.openai.com/api-keys).

Save the OpenAI API key as an environment variable:

```bash
read -s OPENAI_API_KEY
export OPENAI_API_KEY
echo $OPENAI_API_KEY
```

Set the model to use 0613 (or later) via `export OPENAI_DEPLOYMENT_NAME=gpt-3.5-turbo-0613`.

Create alias:

```bash
alias kai='kubectl kubectl-ai'
```

### Use with external editors

```bash
# Visual Studio Code
kai "create a foo namespace" --raw | code -
```

## Examples

| NAME | PROMPT | DESCRIPTION | EXAMPLE |
| ---- | ------ | ----------- | ------- |
| Pod | "Create pod app with port 8000" | Defines a K8s Pod for app deployment with a container exposing port 8000. | [`app.yaml`](/yaml/app.yaml) |
| Liveness | "Create app liveness probe get ports 8080:8000 with times" | Defines a K8s Pod with liveness probe for app on port 8080. | [`app-livenessProbe.yaml`](/yaml/app-livenessProbe.yaml) |
| Readiness | "Create app readiness probe get ports 8080:8000 with times" | Defines a K8s Pod with readiness probe for app on port 8080. | [`app-readinessProbe.yaml`](/yaml/app-readinessProbe.yaml) |
| Volumes | "Create app volume mounts with path mount /data host /var/lib/app" | Defines a K8s Pod for app with data volume mounted at /data. | [`app-volumeMounts.yaml`](/yaml/app-volumeMounts.yaml) |
| CronJob | "Create app cronJob every 5 min" | Defines a K8s CronJob for running a task every 5 minutes using image and command. | [`app-cronjob.yaml`](/yaml/app-cronjob.yaml) |
| Job | "Create app Job from image with volumes" | Defines a K8s Job with two containers using volumes, one writable and one read-only. | [`app-job.yaml`](/yaml/app-job.yaml) |
| Multicontainer | "Create app multi container nginx and debian with volumes" | Defines a K8s Pod with two containers: nginx on port 80 and Debian sharing data in /app/shared. | [`app-multicontainer.yaml`](/yaml/app-multicontainer.yaml) |
| Resources | "Create app resources cpu 100m and memory 128-256Mi" | Defines a K8s Pod with resource limits and requests for CPU and memory. | [`app-resources.yaml`](/yaml/app-resources.yaml) |
| app-secret-env | ""Create app redis pod with volume secret"" | Defines a K8s Pod running Redis with a mounted read-only secret volume. | [`app-secret-env.yaml`](/yaml/app-secret-env.yaml) |
