###  installation (UNE fois)


helm repo add argo https://argoproj.github.io/argo-helm
helm repo update

helm install argocd argo/argo-cd \
  -n argocd --create-namespace \
  -f argocd/values.yaml

### appliquer UNE fois

kubectl apply -f bootstrap/root-app.yaml

### Créer .env 

nano .env

source .env

### Créer le secret


kubectl create secret docker-registry scw-registry-secret \
  --docker-server=rg.fr-par.scw.cloud \
  --docker-username=$SCW_ACCESS_KEY \
  --docker-password=$SCW_SECRET_KEY \
  -n insurance-sandbox

kubectl create secret docker-registry scw-registry-secret \
  --docker-server=rg.fr-par.scw.cloud \
  --docker-username=$SCW_ACCESS_KEY \
  --docker-password=$SCW_SECRET_KEY \
  -n insurance-build

  kubectl create secret docker-registry scw-registry-secret \
  --docker-server=rg.fr-par.scw.cloud \
  --docker-username=$SCW_ACCESS_KEY \
  --docker-password=$SCW_SECRET_KEY \
  -n insurance-prod


### Créer namespace

kubectl create namespace traefik

### Forcer le sync


kubectl patch application traefik -n argocd \
  --type merge \
  -p '{"operation":{"sync":{}}}'
