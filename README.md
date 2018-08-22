# Example Voting App

The aim of this project is to deploy an example voting app on any docker orchestrator (Docker Swarm, Kubernetes, Openshift)

## Description

This repository is forked from that [repository](https://github.com/dockersamples/example-voting-app).

The voting app is based on that architecture :

*   A Python webapp which lets you vote between two options
*   A Redis queue which collects new votes
*   A .NET worker which consumes votes and stores them in…
*   A Postgres database backed by a Docker volume
*   A Node.js webapp which shows the results of the voting in real time

The architecture can be schematized like this :

![Architecture diagram](docs/images/architecture.png)

Be aware that the voting application only accepts one vote per client. It does not register votes if a vote has already been submitted from a client.

## Getting Started

These instructions will get you a copy of the project up and running on your cluster for development and testing purposes.

### Prerequisites

What things you need to deploy this app :

*   You need to provision the cluster on which you want to deploy the app
*   You need to be qble to management of your cluster with the command line (kubectl, oc, docker)

## Usage

Depending on the Docker orchestrator that you choose, the deploment methode may be different.

### Docker (local deployment)

Move to the folder deployments/docker qnd run this command :

```
docker-compose up
```

The app will be running at [http://localhost:5000](http://localhost:5000), and the results will be at [http://localhost:5001](http://localhost:5001).

### Docker Swarm

The folder deployments/swarm contains the yaml specifications of the Voting App's services. Move to that folder and run this command :

```
docker stack deploy --compose-file docker-stack.yml vote
```

### Kubernetes

The folder deployments/kubernetes contains the yaml specifications of the Voting App's services.

Run the following command to create the deployments and services objects:

```
$ kubectl apply -f deployments/kubernetes/
deployment "db" created
service "db" created
deployment "redis" created
service "redis" created
deployment "result" created
service "result" created
deployment "vote" created
service "vote" created
deployment "worker" created
```

The vote interface is then available on port 31000 on each host of the cluster, the result one is available on port 31001.

### Openshift

The folder deployments/openshift contains the yaml specifications of the Voting App's services.

Run the following command to create the deployments and services objects:
```
$ oc apply -f deployments/openshift/
deployment "db" created
service "db" created
deployment "redis" created
service "redis" created
deployment "result" created
service "result" created
deployment "vote" created
service "vote" created
deployment "worker" created
```

The vote interface is then available on port 31000 on each host of the cluster, the result one is available on port 31001.
