# install-argocd-openshfit
  - oc apply -f argocd-install.yaml -n argo-test
# delete deployment 
  - oc delete -f argocd-install.yaml -n argo-test

 # to deploy Vault in openShfit  Cluster
   - oc create namespace vault
   - oc project vault
   - helm repo add hashicorp https://helm.releases.hashicorp.com
   - helm search repo hashicorp/vault
   - helm install vault hashicorp/vault
   - oc port-forward vault-0 8200:8200
