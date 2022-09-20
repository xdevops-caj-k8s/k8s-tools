# odo

Use odo 3.0 and OpenShift for this demo.

**Pros.**
- Fast build, deploy and run your application in kubernetes cluster
- Auto rebuild, redeploy your application once the source codes changed
- Auto delete/recycle kubernetes resource once exit odo development mode
- Every developer can have his indepent working namespace in kubernetes
- Don't require pipeline
- Don't need write container file and kubernetes YAML fiels

**Cons.**
- Only work for **inner development loop** for local development (code-build-deploy-test)
- A shared development kubernetes cluster with enough resouces


Inner development loop means local coding, build, deploy and test before commit code changes.

![inner_development_loop](https://developers.redhat.com/sites/default/files/styles/article_floated/public/blog/2020/05/To-Staging.png)



## Install odo

References:
- https://odo.dev/docs/overview/installation

Install `odo` on MacOS:

```bash
# download
curl -L https://developers.redhat.com/content-gateway/rest/mirror/pub/openshift-v4/clients/odo/v3.0.0~rc1/odo-darwin-amd64 -o odo

chmod +x ./odo
sudo mv ./odo /usr/local/bin/odo

# verify
odo version
```

## Developing with Java (Spring Boot)

References:
- https://odo.dev/docs/user-guides/quickstart/java

### Step 1. Connect to your cluster and create a new namespace or project

Login to OpenShift Cluster:
```bash
# copy login command, replace `oc login --token` as `odo login --token`
odo login --token ...
```

Create a new OpenShift project:
```bash
odo create project spring-demo
```

### Step 2. Initializing your application

```bash
odo init
```

A `devfile.yaml` has now been added to your directory and now you're ready to start development.

### Step 3. Developing your application continuously

```bash
odo dev
```

The `odo dev` executes `build`, `deploy` and `run`.

- `build`: Build application and image
- `deploy`: Deploy application to project in cluster
- `run`: Run application in cluster and forward service to lcoal port

Access local port `127.0.0.1:40001` to access your application.

The `odo dev` command watches the local project folder, once the source codes changed, it will auto trigger rebuilds and redeploys.

The following kubernetes resources are created in the project:
- PVC
    - `m2-xxx` for Maven local repo cache in container
    - `odo-projects-xxx` fro odo data
- Deployment
- Service

Press Ctrl+c to exit `odo dev` and delete kuberentes resources from the cluster.

