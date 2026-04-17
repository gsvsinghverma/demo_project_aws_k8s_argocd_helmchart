-------------------------
Run On Jump Server
-------------------------

ssh -i bastion-key.pem ubuntu@<JUMP_SERVER_IP>


EKS cluster connect verify

-----------------------------------------------------------------------------
kubectl get nodes
-----------------------------------------------------------------------------

*******************************************
Install via Helm
*******************************************



kubectl create namespace argocd

helm repo add argo https://argoproj.github.io/argo-helm
helm repo update

helm install argocd argo/argo-cd \
  --namespace argocd \
  --set server.service.type=LoadBalancer

# Wait for pods
kubectl get pods -n argocd -w



********************************************
Get Password & URL
********************************************


# Password
kubectl -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath="{.data.password}" | base64 -d

# URL (EXTERNAL-IP copy karo)
kubectl get svc -n argocd argocd-server


************************************
ArgoCD CLI + GitHub Connect
************************************
# CLI Install
curl -sSL -o argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
chmod +x argocd && sudo mv argocd /usr/local/bin

# Login
argocd login <ARGOCD-EXTERNAL-IP> --username admin --password <password> --insecure

# GitHub Repo Connect
argocd repo add https://github.com/your-org/your-repo \
  --username your-github-user \
  --password your-github-token

# App Create
argocd app create gsv-app \
  --repo https://github.com/your-org/your-repo \
  --path helm/gsv-app \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default \
  --sync-policy automated


