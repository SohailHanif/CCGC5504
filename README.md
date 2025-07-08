# CCGC5504 Repo

This repo will contain code snippets and files for CCGC5504

<br>

# Commands

## Git
### First time using Git 
```
git config --global user.name "YOUR_NAME"
git config --global user.email "YOUR_EMAIL"
```

### Creating new repo 
```
git init
git remote add origin GITHUB_REPO_URL
```

### Using existing repo
```
git clone GITHUB_REPO_URL
```

### When making changes (Most Used) 
```
git add .
git commit -m "commit message"
git push origin master
git pull origin master
```

### Adding new feature that want to seperate from main code until it is finished
```
git branch NEW_BRANCH_NAME
git checkout NEW_BRANCH_NAME
git push origin NEW_BRANCH_NAME
```

### When feature done and ready to merge to main branch
```
git checkout master
git merge NEW_BRANCH_NAME
git push origin master
```


## Docker

### Installation
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
```

### Run Container
```
sudo docker run hello-world
```


### Get Compose Example
```
git clone https://github.com/iimran-muhammad/multi-container-app
```

### Compose
```
sudo docker compose up
sudo docker compose down
```


## Kubernetes

### Installation
```
curl -sfL https://get.k3s.io | sh - 
```

### Get Components
```
sudo k3s kubectl get node
sudo k3s kubectl get pods -A
sudo k3s kubectl get services -A
sudo k3s kubectl get deployments -A
sudo k3s kubectl get namespace --show-labels
```

### Deploy App
```
sudo k3s kubectl apply -f nginx.yml 
sudo k3s kubectl get pods -n default
sudo k3s kubectl get services -n default
```

### Destroy/ Redeploy App
```
sudo k3s kubectl delete -f nginx.yml 
```

### Debugging Failed resource
#### Any resource
```
sudo k3s kubectl -n default describe pod basic-pods
sudo k3s kubectl -n default describe pod basic-pods > debug.txt
```

#### Pods only
```
sudo k3s kubectl -n default logs basic-pods
```

## Helm

### Installation
```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

### Creating Charts/Applications
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

### Getting Kubernetes Context

```
mkdir $HOME/.kube/
sudo cat /etc/rancher/k3s/k3s.yaml > $HOME/.kube/config
```

### Installing from ArtifactHub
https://artifacthub.io/packages/helm/bitnami/wordpress

```
Direct Install

helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-wordpress bitnami/wordpress -
```

```
Download locally
helm pull oci://registry-1.docker.io/bitnamicharts/wordpress --version 25.0.0
```


### Aliases
```
echo "alias k='sudo k3s kubectl'" >> ~/.bashrc  && source  ~/.bashrc
echo "alias helm='sudo helm'" >> ~/.bashrc  && source  ~/.bashrc
```