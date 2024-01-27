# TODO App with Helm Chart
#### Authors: Tobias Buhmann, Mustafa Rafie
The app and docker image used for this assignment were already built in Task 2 - Kubernetes Manifests. \
Repository URL: `https://github.com/cloud-native-uas/task-2-kubernetes-manifests-group_e`

## Description
The application provides an overview of a user's tasks. Users can easily create new tasks, mark them as completed or delete them. \
Instead of deploying the application with `kubectl` (as we did in Task 2), we decided to create a Helm chart for deployment. This makes deployment much simpler, as the various YAML files no longer need to be executed individually and in sequence. Helm Charts allow easy maintenance of application settings in a single YAML file. This is particularly useful during upgrades and helps to avoid potential misconfigurations.

## Setup
### Kubernetes Context
#### Set Context
`kubectl config use-context docker-desktop`

### Kubernetes Namespace
#### Create Namespace
`kubectl create namespace todo-app-group-e`

#### Set Namespace
`kubectl config set-context --current --namespace=todo-app-group-e`

### Helm Chart
Source: ChatGPT
#### Installation
Depends on your operating system. On windows the easiest way is to install it with Chocolatey Package Manager. \
`choco install kubernetes-helm`

#### Create Helm Chart
`helm create todo-app-group-e`

#### Update Files
`Chart.yaml` & `values.yaml`

#### Validate Helm Chart
`helm lint`

#### Deploy Application Using Helm Chart
`helm install todo-app-group-e .\todo-app-group-e`

#### Test Application
1. Save POD_NAME variable: \
`$env:POD_NAME = (kubectl get pods --namespace todo-app-group-e -l "app.kubernetes.io/name=todo-app-group-e,app.kubernetes.io/instance=todo-app-group-e" -o jsonpath="{.items[0].metadata.name}")`
2. Save CONTAINER_PORT variable: \
`$env:CONTAINER_PORT = (kubectl get pod --namespace todo-app-group-e $env:POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")`
4. Port-forwarding to access application through `localhost:8080`: \
`kubectl --namespace todo-app-group-e port-forward $env:POD_NAME 8080:$env:CONTAINER_PORT`
