# Applications Deployment with ArgoCD
#### Authors: Tobias Buhmann, Mustafa Rafie
The app and docker image used for this assignment was already built in Task 2 - Kubernetes Manifests. \
Repository URL: `https://github.com/cloud-native-uas/task-2-kubernetes-manifests-group_e`

### Context
#### Set Context
`kubectl config use-context docker-desktop`

### Namespace
#### Create Namespace
`kubectl apply -f argocd-namespace.yml`

#### Set Namespace
`kubectl config set-context --current --namespace=argocd` \
`kubectl config get-contexts`

### ArgoCD
#### Installation
`kubectl create -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml -n argocd`

#### Port-Forwarding to access UI
`kubectl port-forward svc/argocd-server -n argocd 8080:443`

#### Get Password
`(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}") | ForEach-Object { [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_)) }`

### Service
#### Create Service
`kubectl apply -f service.yml` \
`kubectl get service -o wide`

### Deployment
`kubectl apply -f deployment.yml` \
`kubectl rollout status deployment/todo-app-group-e-deployment`