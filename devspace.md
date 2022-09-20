# devspace

Use devspace and OpenShift for this demo.

## Install devspace

References:
- https://devspace.sh/docs/getting-started/installation

```bash
# download
curl -L -o devspace "https://github.com/loft-sh/devspace/releases/latest/download/devspace-darwin-amd64"

chmod +x devspace
sudo install devspace /usr/local/bin

# verify
devspace version
```

## Initialize a Project

References:
- https://devspace.sh/docs/getting-started/initialize-project

```bash
devspace init
```

Select
- Select the programming language of this project: `java-maven`
- How do you want to deploy this project? `helm`
- Do you already have a Helm chart for this project? `No`
- Do you want to develop this project with DevSpace or just deploy it? `I want to develop ...`
- How should DevSpace build the container image for this project? `Skip / I dont know`
- Which port is your application listening on? (Enter to skip) `Skip`

## Development with DevSpace

References:
- https://devspace.sh/docs/getting-started/development

## Login Cluster

Login to OpenShift Cluster:
```bash
# copy login command
oc login --token ...
```

## Create a new OpenShift project
Create a new OpenShift project:
```bash
odo create project spring-demo
```

### Choose Cluster & Namespace

Check current OpenShift context:
```bash
oc config current-context
```


```bash
# swithc context (cluster)
devspace use context

# switch namespace
devspace use namespace springboot-demo
```

### Start Dev Container

```bash
devspace dev
```

Known issues:
- Failed to download helm chart due to network issue...

## Following steps

TBC


## Compare with OpenShift odo

odo is easier to use than devspace.

