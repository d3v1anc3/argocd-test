# Access Argo-CD UI

> **Security Notice:**  
> For security reasons, the Argo CD UI is **not exposed via Ingress** and should only be accessed through a secure, temporary `kubectl port-forward` session. This ensures the UI is only available locally to authenticated cluster users.

## 1. Start Port Forwarding
Run the following command in your terminal or PowerShell:

```powershell
kubectl -n argocd port-forward svc/argocd-server 8080:443
```

This forwards your local port `8080` to the Argo CD server's HTTPS port (`443`) inside the cluster.

Keep this terminal window open while using the UI.

## 2. Open the Argo CD UI
In your browser, go to:

```
https://127.0.0.1:8080
```

## 3. Log In
Login with **username:** `admin` and the **password**

---

## 4. End the Session
When you finish using Argo CD, press `Ctrl + C` in the port-forward terminal window to close the session.
