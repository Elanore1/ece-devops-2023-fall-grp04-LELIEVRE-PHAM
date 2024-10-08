# ece-devops-2023-fall-grp04-LELIEVRE-PHAM
# User API web application

It is a basic NodeJS web application exposing REST API that creates and stores user parameters in [Redis database](https://redis.io/).

## Functionality

1. Start a web server
2. Create a user
3. Create/Get a user
4. Vagrant
5. Ansible
6  Docker
7. Docker Compose
8. Kubernetes


## Installation

This application is written on NodeJS and it uses Redis database.

1. [Install NodeJS](https://nodejs.org/en/download/)

2. [Install Redis](https://redis.io/download)

3. [Install Docker](https://docs.docker.com/engine/install/)

4. [Install Minikube](https://kubernetes.io/fr/docs/tasks/tools/install-minikube/)
    
5. [Install Vagrant](https://developer.hashicorp.com/vagrant/install?product_intent=vagrant)


6. Install application

Go to the root directory of the application (where `package.json` file located) and run:

```
npm install 
```

## UserApi

1. Start a web server

From the root directory of the project run:

```
npm start
```

It will start a web server available in your browser at http://localhost:3000.

![Screenshot](images/Hello%20World.png)


2. Create a user

![Screenshot](images/new%20user.png)

Send a POST (REST protocol) request using terminal:

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{"username":"sergkudinov","firstname":"sergei","lastname":"kudinov"}' \
  http://localhost:3000/user
```

It will output:

```
{"status":"success","msg":"OK"}
```

![Screenshot](images/check%20user.png)

Another way to test your REST API is to use [Postman](https://www.postman.com/).

## Testing

From the root directory of the project, run:

```
npm test
```

![Screenshot](images/npm%20test.png)

## CI/CD Pipeline

We made this part using a workflow from Github Action , each time a new push is made on the main branch , the workflow will check if the userapi still works and if it's able to connect to the redis database

![Screenshot](images/githubactions.png)


## Vagrant / Ansible

1. From the iac folder , run:

```
vagrant up
```
You can see during the start of the machine the installation of Ansible and the healthchecks from the playbooks

![Screenshot](images/ansiblehealthcheck.png)


2. From there you can access the terminal of vagrant with SSH using:

```
vagrant ssh
```


3. You should be able to see the files of the app inside the container using :

```
ls
```

![Screenshot](images/Vagrant%20SSH.png)


## Docker and Docker Compose

You can either build the image from the userapi folder using :

```
docker build . 
```

Or pull the image from the Docker repository (it will take the latest tag) :

![Screenshot](images/DockerPush.png)

```
docker pull noepham/eceuserapi
```

Then build the image from the image you just pulled :

```
docker run noepham/eceuserapi
```

Afterwards , you should be able to use the image if you have redis running in the background:


IF you want to start the application directly from the root of the repository you can run:

```
docker-compose up
```
![Screenshot](images/Docker%20compose%20launches.png)

The application should be up and ready to use :

![Screenshot](images/localhost8000.png)
![Screenshot](images/localhost8000user.png)




## Kubernetes 

Start by using the minikube start command from the k8s folder:

```
minikube start
```

You will then need to run the deployment , service and persitent-volume and persistent-volume-claim to run the app:

```
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f persistent-volume-claim.yaml
kubectl apply -f persistent-volume.yaml
```

You should be able to find the url of the service using:

```
minikube service eceuserapi-service or
minikube service eceuserapi-service --url
```
![Screenshot](images/serviceeceuserapi.png)

Then you can start using the new ip using the same command but adapting the url:

```
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{"username":"sergkudinov","firstname":"sergei","lastname":"kudinov"}' \
  <Minikube-Service-URL>/user
```

![Screenshot](images/kubernetesapp.png)

Then you can try to delete the deployments and service and see that the data is still present:

![Screenshot](images/persistentvolume.png)



## Istio


## Monitoring













