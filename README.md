# install-argocd-openshfit
  - oc login --token= ... --server= ....
  - oc project argo-test
  - oc apply -f argocd-install.yaml -n argo-test
  - oc apply -f argocd-vault-plugin-credentials.yaml -n argo-test
  - oc apply -f argocd-helm-values.yaml -n argo-test
  - oc apply -f argocd-vault-plugin-cmp.yaml -n argo-test
    
# delete deployment 
  - oc delete -f argocd-install.yaml -n argo-test

 # to deploy Vault in openShfit  Cluster
   - oc create namespace vault
   - oc login --token= ... --server= ....
   - oc project vault
   - helm repo add hashicorp https://helm.releases.hashicorp.com
   - helm search repo hashicorp/vault
   - helm install vault hashicorp/vault
   - oc port-forward vault-0 8200:8200
   - oc login --token= ... --server= ....
   - vault login -address= ... vault URL.. -tls-skip-verify      if not accept to login use this
   - echo | openssl s_client -connect .....vault URL...... | openssl x509 -out /tmp/vault-cert.crt
   - sudo cp /tmp/vault-cert.crt /usr/local/share/ca-certificates/vault-cert.crt
   - sudo update-ca-certificates
   - export VAULT_CACERT=/path/to/vault-cert.crt
   - vault login -address=..vault URL....
   - vault write auth/approle/role/vault-plugin-role \
    token_type=service \
    secret_id_ttl=10m \
    token_num_uses=10 \
    token_ttl=20m \
    token_max_ttl=30m \
    secret_id_num_uses=40
   -  vault read auth/approle/role/vault-plugin-role/role-id
   -  vault write -f auth/approle/role/vault-plugin-role/secret-id
