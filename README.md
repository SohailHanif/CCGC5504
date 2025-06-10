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
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
sudo usermod -aG docker $USER && newgrp docker

## Start
minikube start

## Get Components
minikube kubectl -- get pods -A
minikube kubectl -- get services -A
minikube kubectl -- get deployments -A

## Deploy App
minikube kubectl -- apply -f nginx.yml 