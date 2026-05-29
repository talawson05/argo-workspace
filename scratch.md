k3d cluster create mycluster
k3d cluster delete mycluster
k3d cluster list
k3d cluster stop mycluster
k3d cluster start mycluster


k3d cluster create mycluster \
  -p "80:80@loadbalancer" \
  -p "443:443@loadbalancer" \
  --k3s-arg "--disable=traefik@server:0"




helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
helm install argocd argo/argo-cd -n argocd --create-namespace

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

kubectl port-forward svc/argocd-server -n argocd 8080:443
kubectl port-forward svc/argocd-server -n argocd 9090:443

http://localhost:8080
http://localhost:9090


kubectl config set-context --current --namespace=argocd
brew install argocd
argocd login --core
argocd app list

argocd app sync root-echo-apps



helm repo add podinfo https://stefanprodan.github.io/podinfo
helm repo update
helm install first-echo podinfo/podinfo --set ui.message="Yo" --set service.type=ClusterIP
helm install second-echo podinfo/podinfo --set ui.message="Yo yo" --set service.type=ClusterIP


kubectl apply -f ./bootstrap/root-app.yaml


% kubectl create namespace gravitee namespace/gravitee created 
% kubens argocd Context "minikube" modified. Active namespace is "argocd". 
% argocd app create graviteegitopsapis --repo https://github.com/jmcx/gravitee-quickstart.git --path 05_GitOps_ArgoCD/resources --dest-server https://kubernetes.default.svc --dest-namespace gravitee application 'graviteegitopsapis' created


echo "127.0.0.1 apim.localhost" | sudo tee -a /etc/hosts
echo "127.0.0.1 api.localhost" | sudo tee -a /etc/hosts  
echo "127.0.0.1 dev.localhost" | sudo tee -a /etc/hosts


http://apim.localhost/console
http://dev.localhost/

curl http://api.localhost/


kubectl config set-context --current --namespace=gravitee
kubectl port-forward svc/gravitee-apim-gateway 8082:82 -n gravitee
kubectl port-forward service/gravitee-apim-ui 8002:8002 -n gravitee
kubectl port-forward service/gravitee-apim-portal 8003:8003 -n gravitee


curl http://localhost:8082/
http://localhost:8002/console
http://localhost:8003/



kubectl get ingress -n gravitee

