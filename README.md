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

## Verify that the policies applied

Check the running application for image tags:

```sh
kubectl -n demo get pod -o yaml | grep "image:"
```

This should show that images are references using digests:

```yaml
    - image: ghcr.io/nirmata/demo-argocd:v1@sha256:b31bfb4d0213f254d361e0079deaaebefa4f82ba7aa76ef82e90b4935ad5b105
      image: sha256:f9d5de0795395db6c50cb1ac82ebed1bd8eb3eefcebb1aa724e01239594e937b
```
Check the running application for service accounts:

This command will check for any volumes and if automountServiceAccountToken is disabled.

```sh
kubectl -n demo get pod -o yaml | grep -i "serviceAccountToken"
```

The output should only contain instructions to turn off the auto-mounting of service account tokens:

```yaml
    automountServiceAccountToken: false
```

Check the running application for cluster autoscaler annotations:

This command will check the pod annotations:

```sh
kubectl -n demo get pod -o yaml | grep -i "annotations" -A1
```

The output should show the “cluster-autoscaler.kubernetes.io/safe-to-evict: true” annotation:

```yaml
    annotations:
      cluster-autoscaler.kubernetes.io/safe-to-evict: "true"
```
