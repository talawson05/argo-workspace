k3d cluster create mycluster
k3d cluster delete mycluster
k3d cluster list
k3d cluster stop mycluster
k3d cluster start mycluster




helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
helm install argocd argo/argo-cd -n argocd --create-namespace

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

kubectl port-forward svc/argocd-server -n argocd 8080:443
http://localhost:8080


helm repo add podinfo https://stefanprodan.github.io/podinfo
helm repo update
helm install first-echo podinfo/podinfo --set ui.message="Yo" --set service.type=ClusterIP
helm install second-echo podinfo/podinfo --set ui.message="Yo yo" --set service.type=ClusterIP


