# demo-argocd
ArgoCD demo app

## Create a kind Cluster

[Install kind](https://kind.sigs.k8s.io/) and create a cluster:

```sh
kind create cluster --name=kyverno-argocd
```

## Install Kyverno

```sh
kubectl create -f https://github.com/kyverno/kyverno/raw/main/config/install-latest-testing.yaml
```

## Install Kyverno Policies

```sh
kubectl apply -f https://raw.githubusercontent.com/nirmata/demo-argocd-kyverno/main/config/kyverno-policies.yaml
```

## Install ArgoCD

```sh
kubectl create ns argocd
```

```sh
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.10.0-rc1/manifests/install.yaml
```

## Create the ArgoCD Application

```sh
kubectl apply -f https://raw.githubusercontent.com/nirmata/demo-argocd-kyverno/main/config/argocd-app/application.yaml
```

