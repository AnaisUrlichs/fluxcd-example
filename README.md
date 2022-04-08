# Flux exmaple to manage Helm Chart Deployment and Application

Please refer to the Flux documentation for [installation options.](https://fluxcd.io/docs/installation/)

You can find the blog post for this repository here:
AND the YouTube tutorial: 

## Installing the Starboard Helm Chart

The Starboard Helm Chart can either be deployed through the following commands:
```
flux create source helm starboard-operator --url https://aquasecurity.github.io/helm-charts/ --namespace starboard-system
flux create helmrelease starboard-operator --chart aqua/starboard-operator \
  --source HelmRepository/starboard-operator \
  --chart-version 0.10.3 \
  --namespace starboard-system
```

OR declaratively by deploying [helm-starboard.yaml](helm-starboard.yaml)
```
kubectl apply -f helm-starboard.yaml
```

## Installing an application through Flux

We are going to install the Kubernetes manifests from the following [Git repository](https://github.com/AnaisUrlichs/react-article-display): 

You can find the Flux installation in [application.yaml](application.yaml)

```
kubectl apply -f application.yaml
```

### Using the Flux bootstrap command

Similar to how you can deploy applications through ArgoCD, you can deploy an application directly through the Flux CLI.

```
flux create source git react \
    --url=https://github.com/AnaisUrlichs/react-article-display \
    --branch=main
```

```
flux create kustomization react-app \
  --target-namespace=app \
  --source=react \
  --path="./manifests" \
  --prune=true \
  --interval=5m \
```