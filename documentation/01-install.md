# 01 - Install Argo Rollouts

Argo Rollouts is a Kubernetes controller and set of CRDs which provide advanced deployment capabilities such as blue-green, canary, canary analysis, experimentation, and progressive delivery features to Kubernetes. 

Official documentation :

- https://argoproj.github.io/argo-rollouts/

## Install with helm

Helm github repo :

- https://github.com/argoproj/argo-helm/tree/master/charts/argo-rollouts

First fetch the Chart :
```
helm repo add argo https://argoproj.github.io/argo-helm
helm fetch --untar argo/argo-rollouts
```

And then install it :

```
helm upgrade -i argo-rollouts -n argocd argo-rollouts/ --set dashboard.enabled=true --set metrics.enabled=true --set metrics.serviceMonitor.enabled=true
```

If you want to see the dashboard, you need to expose `argo-rollouts-dashboard` service with ingress/route. You can find Traefik `IngressRoute` example [here](../resources/yaml/ingressroute-argo-rollout.yaml)

If you use ArgoCD for deployment, you can override values for ServiceMonitor:
```yaml
controller:
  metrics:
    enabled: true
    serviceMonitor:
      enabled: true
      additionalLabels:
        release: prom
```

## Install kubectl plugin

You can also install the kubectl plugin :

```
curl -LO https://github.com/argoproj/argo-rollouts/releases/latest/download/kubectl-argo-rollouts-linux-amd64
chmod +x ./kubectl-argo-rollouts-linux-amd64
sudo mv ./kubectl-argo-rollouts-linux-amd64 /usr/local/bin/kubectl-argo-rollouts
```

And check the version
```
kubectl argo rollouts version
```