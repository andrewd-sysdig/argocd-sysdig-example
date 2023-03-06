# How to setup ArgoCD to deploy sysdig-agent

## Install ArgoCD to your kubernetes cluster via helm
```sh
helm repo add argo https://argoproj.github.io/argo-helm
helm install argocd --create-namespace --namespace argocd argo/argo-cd
```

## Create the sysdig-agent Argo Application
Version 2.6+ of ArgoCD is required as this introduces a new feature that allows you to specify your helm values.yaml to come from a different repository than the helm chart. See: https://argo-cd.readthedocs.io/en/stable/user-guide/multiple_sources/#helm-value-files-from-external-git-repository

Create 2 secrets, one for your Sysdig AccessKey and one for your Sysdig API Token (no these aren't real)
```sh
kubectl create -n sysdig-agent secret generic sysdig-access-key --from-literal access-key=235af419-e0f7-43af-b271-094a50c6e0aa
kubectl create -n sysdig-agent secret generic sysdig-api-token --from-literal SECURE_API_TOKEN=f1fc4ea1-322e-43cb-bafc-9737e00a44fa
```

Now clone this repo and apply the ArgoCD Application

```sh
git clone https://github.com/andrewd-sysdig/argocd-sysdig-example.git
kubectl apply -f ~/prod/prod-cluster-values.yaml
```
