###  installation (UNE fois)


helm repo add argo https://argoproj.github.io/argo-helm
helm repo update

helm install argocd argo/argo-cd \
  -n argocd --create-namespace \
  -f argocd/values.yaml

### appliquer UNE fois

kubectl apply -f bootstrap/root-app.yaml