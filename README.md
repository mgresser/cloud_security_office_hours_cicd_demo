# cloud_security_office_hours_cicd_demo
Demo CICD Project for Cloud Security Office Hours

This project is designed to enable a simple demo to show a very simple example of common CICD practices with regards to vulnerabilty scanning as well as to show common cloud deployment patterns. This should not be used in production, for demo only.

This project contains a CICD pipeline that will build a container once it passes a vulnerability scan done with Clair.

Once built we will deploy the updated resources into our environment using ArgoCD and show the changes.

Prerequisites:
Github account
Docker Account
ArgoCD CLI tool installed (brew install argocd on macs)
Docker for Desktop with a kubernetes cluster.

Steps:
Clone repo
Create service account in Docker Hub to use to upload images.
Create secrets in Github for the DockerHub credentials.
Enable Kubernetes in Docker for Desktop
Install argocd cli tool
`brew install argocd`
Deploy ArgoCD into your cluster
`kubectl create namespace argocd`
`kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`
Expose ArgoCD on port 8080
`kubectl port-forward svc/argocd-server -n argocd 8080:443`
Get initial admin credentials
`argocd admin initial-password -n argocd`
Add the docker-desktop cluster to ArgoCD
`argocd cluster add docker-desktop`
Create namespace for the demo app
`kubectl create namespace demo`
Log into https://localhost:8080
New App
Name the App
Select Default Project
Set sync policy to automatic
Copy git repo link to Repository URL
Set revision to HEAD
Set path to /k8s
Select cluster docker.internal
Set namespace to demo