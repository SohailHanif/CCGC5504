# CCGC5504 Repo

This repo will contain code snippets and files for CCGC5504

# Git
## First time using Git 
```
git config --global user.name "YOUR_NAME"
git config --global user.email "YOUR_EMAIL"
```

## Creating new repo 
```
git init
git remote add origin GITHUB_REPO_URL
```

## Using existing repo
```
git clone GITHUB_REPO_URL
```

## When making changes (Most Used) 
```
git add .
git commit -m "commit message"
git push origin master
git pull origin master
```

## Adding new feature that want to seperate from main code until it is finished
```
git branch NEW_BRANCH_NAME
git checkout NEW_BRANCH_NAME
git push origin NEW_BRANCH_NAME
```

## When feature done and ready to merge to main branch
```
git checkout master
git merge NEW_BRANCH_NAME
git push origin master
```

# Public IP address
```
curl ipinfo.io/ip
```

# Docker

## Installation
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
```

## Run Container
```
sudo docker run hello-world
```


## Get Compose Example
```
git clone https://github.com/iimran-muhammad/multi-container-app
```

## Compose
```
sudo docker compose up
sudo docker compose down
```


# Kubernetes

## Installation
```
curl -sfL https://get.k3s.io | sh - 
```

## Get Components
```
sudo k3s kubectl get node
sudo k3s kubectl get pods -A
sudo k3s kubectl get services -A
sudo k3s kubectl get deployments -A
sudo k3s kubectl get namespace --show-labels
```

## Deploy App
```
sudo k3s kubectl apply -f nginx.yml 
sudo k3s kubectl get pods -n default
sudo k3s kubectl get services -n default
```

## Destroy/ Redeploy App
```
sudo k3s kubectl delete -f nginx.yml 
```

## Debugging Failed resource
## Any resource
```
sudo k3s kubectl -n default describe pod basic-pods
sudo k3s kubectl -n default describe pod basic-pods > debug.txt
```

## Pods only
```
sudo k3s kubectl -n default logs basic-pods
```

# Helm

## Installation
```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

## Creating Charts/Applications
```
helm create website
```

```
.
└── website
    ├── Chart.yaml
    ├── charts
    ├── templates
    │   ├── NOTES.txt
    │   ├── _helpers.tpl
    │   ├── deployment.yaml
    │   ├── hpa.yaml
    │   ├── ingress.yaml
    │   ├── service.yaml
    │   ├── serviceaccount.yaml
    │   └── tests
    │       └── test-connection.yaml
    └── values.yaml

5 directories, 10 files
```

## Getting Kubernetes Context

```
mkdir $HOME/.kube/
sudo cat /etc/rancher/k3s/k3s.yaml > $HOME/.kube/config
```

## Installing Directly from ArtifactHub
https://artifacthub.io/packages/helm/bitnami/wordpress

## Commands
```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-wordpress bitnami/wordpress
```

## Output 
```
Your WordPress site can be accessed through the following DNS name from within your cluster:

    my-wordpress.default.svc.cluster.local (port 80)

To access your WordPress site from outside the cluster follow the steps below:

1. Get the WordPress URL by running these commands:

  NOTE: It may take a few minutes for the LoadBalancer IP to be available.
        Watch the status with: 'kubectl get svc --namespace default -w my-wordpress'

   export SERVICE_IP=$(kubectl get svc --namespace default my-wordpress --template "{{ range (index .status.loadBalancer.ingress 0) }}{{ . }}{{ end }}")
   echo "WordPress URL: http://$SERVICE_IP/"
   echo "WordPress Admin URL: http://$SERVICE_IP/admin"

2. Open a browser and access WordPress using the obtained URL.

3. Login with the following credentials below to see your blog:

  echo Username: user
  echo Password: $(kubectl get secret --namespace default my-wordpress -o jsonpath="{.data.wordpress-password}" | base64 -d)

WARNING: There are "resources" sections in the chart not set. Using "resourcesPreset" is not recommended for production. For production installations, please set the following values according to your workload needs:
  - resources
+info https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
```

## Check Status Load Balancer and get public IP
```
k get svc --namespace default -w my-wordpress
```

```
export SERVICE_IP=$(k get svc --namespace default my-wordpress --template "{{ range (index .status.loadBalancer.ingress 0) }}{{ . }}{{ end }}")
echo "WordPress URL: http://$SERVICE_IP/"
echo "WordPress Admin URL: http://$SERVICE_IP/admin"
```

## Download locally from ArtifactHub
```
helm pull oci://registry-1.docker.io/bitnamicharts/wordpress --version 25.0.0
helm install my-wordpress .
```

## Deploy Jenkins
```
helm repo add jenkins https://charts.jenkins.io
helm install my-jenkins jenkins/jenkins --version 5.8.66

mkdir jenkins
helm show values jenkins/jenkins > jenkins/jenkins-values.yml
k get secrets my-jenkins --output json > jenkins/secrets.json

k get secrets my-jenkins --output jsonpath="{.data.jenkins-admin-user}" | base64 --decode
k get secrets my-jenkins --output jsonpath="{.data.jenkins-admin-password}" | base64 --decode

k port-forward --address 0.0.0.0 svc/my-jenkins 81:8080 
```


## Port Forward
k port-forward svc/my-jenkins 81:8080


## Aliases
```
echo "alias k='sudo k3s kubectl'" >> ~/.bashrc  && source  ~/.bashrc
```



# Minimum Commands need to Run
```
echo "Installing Kubernetes"
curl -sfL https://get.k3s.io | sh - 
echo "alias k='sudo k3s kubectl'" >> ~/.bashrc  && source  ~/.bashrc

echo "Installing Helm"
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh

mkdir /home/ubuntu/.kube/
touch /home/ubuntu/.kube/config
sudo cp /etc/rancher/k3s/k3s.yaml /home/ubuntu/.kube/config

k delete deployment traefik -n kube-system
k delete svc traefik -n kube-system

echo "Installing Jenkins"
helm repo add jenkins https://charts.jenkins.io
helm install my-jenkins jenkins/jenkins --version 5.8.66
k get secrets my-jenkins --output jsonpath="{.data.jenkins-admin-password}" | base64 --decode

echo "Running Jenkins"
echo "Wait 10 seconds before connecting to allow finish setup"
sleep 30
k port-forward --address 0.0.0.0 svc/my-jenkins 80:8080 
```

# ArgoCD

## Installation Server
```
k apply -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Installation CLI Command
```
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64
```

## CLI Config
```
argocd login --core
argocd admin initial-password
```

## Access Web UI
```
k port-forward  --address 0.0.0.0 svc/argocd-server 81:443
```

## ArgoCD App management using kubernetes CLI
```
k apply -f week_9/rbac.yml

k apply -f week_9/guestbook.yml

# Access on http://AWS_IP:30082/

k delete -f week_9/guestbook.yml
```

# Helm and ArgoCD
## Create apache app
```
k apply -f week_10/apache/application.yml
k apply -f week_10/helm_apache/application.yml
```


# Github Actions (CI/CD)
## Create your website app with helm apache base
```
k apply -f week_11/sohail_website/application.yml
```

## Create Custom Docker Image and Push to DockerHub
```
sudo docker build -t [DOCKER_HUB_USERNAME]/[REPO_NAME] .
  e.g. sudo docker build -t sohailhanif/sohail-website .

sudo docker push [DOCKER_HUB_USERNAME]/[REPO_NAME]
  e.g. sudo docker push sohailhanif/sohail-website
```


# Observability
## Kubernetes Built-in
```
k get --raw /metrics
k top pod
k top node
```

## Prometheus/Grafana
https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack#configuration

```
helm install my-prometheus-grafana oci://ghcr.io/prometheus-community/charts/kube-prometheus-stack

k get pods -l "release=my-prometheus-grafana"

k get secrets my-prometheus-grafana  -o jsonpath="{.data.admin-user}" | base64 -d ; echo

k get secrets my-prometheus-grafana  -o jsonpath="{.data.admin-password}" | base64 -d ; echo

k port-forward --address 0.0.0.0 svc/my-prometheus-grafana 82:80
```