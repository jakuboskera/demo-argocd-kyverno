# demo-argocd
ArgoCD demo app

## Create a kind Cluster

[Install kind](https://kind.sigs.k8s.io/) and create a cluster:

```sh
kind create cluster --name=kyverno-argocd
```

## Install ArgoCD

```sh
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Install Kyverno

```sh
kubectl create -f https://github.com/kyverno/kyverno/raw/main/config/install-latest-testing.yaml
```

## Install Policies

## Create Application


