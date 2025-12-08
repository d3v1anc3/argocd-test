# Argo CD setup

## Kubernetes
### Create the Azure Key Vault secret
```Powershell
kubectl create secret generic azure-kv-creds --namespace=default --from-literal=clientId='YOUR-AZURE-SP-CLIENT-ID' --from-literal=clientSecret='YOUR-AZURE-SP-CLIENT-SECRET'
```

### Install Argo CD
```powershell
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Get the initial admin password
[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String((kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}")))
```

Save the password in a secure location.

#### Access Argo CD with a Temporary Tunnel
```powershell
kubectl -n argocd port-forward svc/argocd-server 8080:443
```
Open the Argo CD page by going to https://127.0.0.1/8080 and login with username `admin` and the password that you retrieved in the previous step.

#### Load the Argo CD Configuration

```powershell
kubectl apply -f bootstrap/argocd-bootstrap.yaml
```

## References
- [Argo-CD](https://argo-cd.readthedocs.io/en/stable/) - ReadTheDocs