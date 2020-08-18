# Cloud Developer

* [Credentials](#credentials)
* [Docker](#docker)
* [Kubernetes](#kubernetes)
* [Travis](#travis)


## credentials
First, you need to configure your credentials as environment variables in the set_env.sh and add them to travis seting.

export POSTGRES_USERNAME=
export POSTGRES_PASSWORD=
export POSTGRES_HOST=
export POSTGRES_DB=
export AWS_BUCKET=
export AWS_REGION=
export AWS_DEFAULT_REGION=
export AWS_PROFILE=
export JWT_SECRET=
export URL=http://localhost:8080
export AWS_SECRET_ACCESS_KEY=
export AWS_ACCESS_KEY_ID=
export AWS_CONFIG=
export AWS_CREDENTIALS=
export CONFIG=

## docker

you can use docker to test the images locally and use docker-desktop to test create the cluster on kubernetes locally

Also the images were saved on docker hub:

- mmallahham/reverseproxy
- mmallahham/udagram-frontend
- mmallahham/udagram-user
- mmallahham/udagram-feed


## kubernetes
To get kubernetes cluster working, first you need to configure the cluster on AWS, I used AWS EKS, then, you need to run the next command:
- aws eks --region <YOUR_REGION> update-kubeconfig --name <CLUSTER_NAME>
- kubectl get nodes

to use the enviroment variables I use envsubst command (need to install gettext) and this will inject the invironment value in the files when I run kubectl

- envsubst < deployment/k8s/backend-feed-deployment.yaml | kubectl apply -f -

check .travis.yml for more info

you can check the status of the cluster try

- kubectl get pods
- kubectl get svc
- kubectl get deployments

## travis
In the root directory of the github repository, there is a `.travis.yml` that build all the containers then push them to ducker repository, then it run kubectl commands to apply the services and the deployment files automatically.