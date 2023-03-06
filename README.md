# How to setup ArgoCD to deploy sysdig-agent

## Install ArgoCD to your kubernetes cluster via helm
```sh
helm repo add argo https://argoproj.github.io/argo-helm
helm install argocd --create-namespace --namespace argocd argo/argo-cd
```

## Create the sysdig-agent Argo Application
Version 2.6+ of ArgoCD is required as this introduces a new feature that allows you to specify your helm values.yaml to come from a different repository than the helm chart. See: https://argo-cd.readthedocs.io/en/stable/user-guide/multiple_sources/#helm-value-files-from-external-git-repository

Fork this repo and then edit the values.yaml for your sysdig instance. Be careful with your access keys/tokens :)

```sh
git clone https://github.com/andrewd-sysdig/argocd-test.git
kubectl apply -f ~/argocd-test/argocd-sysdig-agent.yaml
```
