# Minikube
Some Fun with Minikube and Helm 

## Initial Install ##

skip anything already installed 

    choco install docker-desktop -y
    choco install minikube -y
    choco install kubernetes-helm -y

Start Minikube

    minikube start

Get the status 

    minikube status


Open CMD - cd into a working directory


OPTIONAL - run this in your terminal to ensure the helm charts repo are added 

    helm repo add  stable     https://charts.helm.sh/stable

Creates the helm chart basic structure (have a browse through to see what it creates)
    
    helm create dadjokes

However just clone this repo...

verify the chart 

    helm lint .\dadjokes\ 

Deploy

    helm install dadjokes dadjokes/ --values dadjokes/values.yaml --create-namespace --namespace=sometest

Upgrade any deployments

    helm upgrade dadjokes dadjokes/ --values dadjokes/values.yaml -i --namespace=sometest

Connect to the deployment

    minikube tunnel

Test via powershell 
    
    Invoke-WebRequest -uri "http://127.0.0.1:8100/" | Select-Object -ExpandProperty content | ConvertFrom-Json | Select-Object -ExpandProperty Joke | Select-Object Opener,Punchline | FT -AutoSize

web browser 

    http://127.0.0.1:8100/


To see the containers etc 

    kubectl get all -A

##Stop the fun ##

The following will delete the helm chart and stop it from running 

    helm list --namespace=sometest
    helm delete dadjokes --namespace=sometest
    helm list  --namespace=sometest


## To look at ##
* Unit Testing https://github.com/helm-unittest/helm-unittest
* https secure page 

## Further Learning ##
* [MiniKube](https://minikube.sigs.k8s.io/docs/start/)
* [DadJokes](https://github.com/yesinteractive/dadjokes)
* [Devops Journey Helm Charts](https://youtu.be/jUYNS90nq8U)
* [What is Helm - IBM](https://www.youtube.com/watch?v=fy8SHvNZGeE)

## Misc Commands ##

    kubectl get pods
    kubectl get replicaset
    kubectl delete services supercooldadjokes --namespace=sometest
    kubectl delete deployment supercooldadjokes --namespace=sometest