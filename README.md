# Running a self-hosted agent in Docker

## Introduction 
You can set up an Azure Pipelines self-hosted agent to run inside a Windows Server Core (for Windows hosts), or Ubuntu container (for Linux hosts) with Docker. This is useful when you want to run agents with some kind of outer orchestration, such as Azure Container Instances. We'll walk through a complete container example, including handling agent self-update.

Both Windows and Linux are supported as container hosts. You'll pass a few environment variables to docker run which configure the agent to connect to Azure Pipelines or Azure DevOps Server. Finally, you'll want to customize the container to suit your needs. Tasks and scripts may depend on specific tools being available on the container's PATH, and it is your responsibility to ensure these tools are available.

## Build DevOps Agent
`docker build -t devopsagent:latest .`

## Run DevOps Agent
```
docker run -e AZP_URL=<Azure DevOps instance> \
           -e AZP_TOKEN=<PAT token> \
           -e AZP_AGENT_NAME=mydockeragent \
           -e AGENT_URL=https://chinare.blob.core.windows.net/agent/vsts-agent-linux-x64-2.172.2.tar.gz (optinal)
           -v /var/run/docker.sock:/var/run/docker.sock \ (optinal)
           devopsagent
```
