[![CircleCI](https://dl.circleci.com/status-badge/img/gh/cstclair252/projectml/tree/main.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/cstclair252/projectml/tree/main)

## Project Overview

In this project, you will apply the skills you have acquired in this course to operationalize a Machine Learning Microservice API. 

You are given a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). This project tests your ability to operationalize a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

This project will use the ability of kubernetes to run the program in a containerized fashion.  This will also make it easy to scale as needed. 


### Project Tasks

Your project goal is to operationalize this working, machine learning microservice using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:
* Test your project code using linting
* Complete a Dockerfile to containerize this application
* Deploy your containerized application using Docker and make a prediction
* Improve the log statements in the source code for this application
* Configure Kubernetes and create a Kubernetes cluster
* Deploy a container using Kubernetes and make a prediction
* Upload a complete Github repo with CircleCI to indicate that your code has been tested

You can find a detailed [project rubric, here](https://review.udacity.com/#!/rubrics/2576/view).

**The final implementation of the project will showcase your abilities to operationalize production microservices.**

---

## Setup the Environment

* Create a virtualenv with Python 3.7 and activate it. Refer to this link for help on specifying the Python version in the virtualenv. 
```bash
python3 -m pip install --user virtualenv
# You should have Python 3.7 available in your host. 
# Check the Python path using `which python3`
# Use a command similar to this one:
python3 -m virtualenv --python=<path-to-Python3.7> .devops
source .devops/bin/activate
```
* Run `make install` to install the necessary dependencies

### Running `app.py`

1. Standalone:  `python app.py`
2. Run in Docker:  `./run_docker.sh`
3. Run in Kubernetes:  `./run_kubernetes.sh`

### Kubernetes Steps

* Setup and Configure Docker locally

install docker 

https://www.docker.com

download the version for you pc and install.


* Setup and Configure Kubernetes locally

Install kubernetes: 

	kubectl Binary: kubectl is the command-line tool for interacting with the Kubernetes cluster. You need to download and install the kubectl binary appropriate for your operating system.
	
	CLI:
		curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
		sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
		
Install Minikube: 
more info go here

	https://minikube.sigs.k8s.io/docs/start/
	
follow these commands. 
	
	curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
	sudo install minikube-linux-amd64 /usr/local/bin/minikube
	
	
	Now you have to start your cluster. 
	
	Cli: 
		Minikube start
		
	
	Interact with your cluster using kubectl. 
	
	Cli: kubectl get po
	Cli: kubectl get pods


* Create Flask app in Container

#you can run the run_docker.sh or you can follow these commands. 

docker build --tag=projectml .

docker run -p 8000:80 projectml

to upload use container to docker hub ./upload_docker.sh


* Run via kubectl

#you can just run the run_kubernetes.sh or here are the commands. 

kubectl run projectml --image=$dockerpath --port=80 --labels=app=projectml

kubectl port-forward projectml 8000:80



## Instructions on how to run the Python scripts and web app:
run_docker.sh - cd into the folder housing the script and run ./run_docker.sh
upload_docker.sh - this will upload file into docker hub make sure to create your own docker hub repo.  run ./upload_docker.sh
run_kubernetes.sh - first you will need to start minikube run minikube start.  Once started you can begin to kubernetes deployment. run ./run_kubernetes


## PROJECT FILES DESCRIPTION:

app.py - python code that execustes prediction.  Extra log file was added "prediction values:"
Dockerfile - file that holds specs on what docker image to use and how to deploy it. copy files to workign directory /app, install packages from requirements, expose ports and command to launch container. 
run_docker.sh - shell script that executes docker build and run parameters
upload_docker.sh - shell script has docker path to upload docker image to the repository on dockerhub
run_kubernetes.sh - shell script that runs kubernetes pod and sets port forward for local machine. 
output files: 
  docker_out - text file with output of foreground program includes new prediction value log output
  kubernetes_out - text file with output of foreground program includes handling connection flag after make prediction was call on another terminal 








