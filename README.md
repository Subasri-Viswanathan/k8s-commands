# k8s-commands
Basic commands for k8s

kubectl set image deployment/id-web-deployment id-web-container=gcr.io/boldreports-dev/bold-identity:4.2.78_24052023_vbasoftware --namespace=bold-services --record

kubectl set image deployment/id-api-deployment id-api-container=gcr.io/boldreports-dev/bold-idp-api:4.2.78_24052023_vbasoftware --namespace=bold-services --record

kubectl set image deployment/id-ums-deployment id-ums-container=gcr.io/boldreports-dev/bold-ums:4.2.78_24052023_vbasoftware --namespace=bold-services --record


kubectl  set image deployment/reports-web-deployment reports-web-container=gcr.io/boldreports-dev/boldreports-server:4.2.78_24052023_vbasoftware --namespace=bold-services --record

kubectl set image deployment/reports-api-deployment reports-api-container=gcr.io/boldreports-dev/boldreports-server-api:4.2.78_24052023_vbasoftware --namespace=bold-services --record

kubectl set image deployment/reports-jobs-deployment reports-jobs-container=gcr.io/boldreports-dev/boldreports-server-jobs:4.2.78_24052023_vbasoftware --namespace=bold-services --record

kubectl set image deployment/reports-reportservice-deployment reports-reportservice-container=gcr.io/boldreports-dev/boldreports-designer:4.2.78_24052023_vbasoftware --namespace=bold-services --record

_______________________________________________________________________________________________


docker build -t bold-identity:4.2.52_06042023_unchain -f bold-identity.txt .	
 
 
docker build -t bold-idp-api:4.2.52_06042023_unchain -f bold-idp-api.txt . 
 
 
docker build -t bold-ums:4.2.52_06042023_unchain -f bold-ums.txt . 
 
 
Report Server 
 
docker build -t boldreports-server:4.2.52_06042023_unchain -f boldreports-server.txt . 
 
 
docker build -t boldreports-server-api:4.2.52_06042023_unchain -f boldreports-server-api.txt . 
 
 
docker build -t boldreports-server-jobs:4.2.52_06042023_unchain -f boldreports-server-jobs.txt . 
 
 
docker build -t boldreports-designer:4.2.52_06042023_unchain -f boldreports-designer.txt . 
  
 
 
  
 Image created in local
 
IDP (Commit the local image to GCR)	
 
docker tag bold-identity:4.2.52_06042023_unchain  gcr.io/boldreports-dev/bold-identity:4.2.52_unchain
 
 
docker tag bold-idp-api:4.2.52_06042023_unchain gcr.io/boldreports-dev/bold-idp-api:4.2.52_unchain 
 
 
docker tag bold-ums:4.2.52_06042023_unchain gcr.io/boldreports-dev/bold-ums:4.2.52_unchain
 
 
Report Server 
 
docker tag boldreports-server:4.2.52_06042023_unchain gcr.io/boldreports-dev/boldreports-server:4.2.52_unchain 
 
 
docker tag boldreports-server-api:4.2.52_06042023_subha gcr.io/boldreports-dev/boldreports-server-api:4.2.52_unchain
 
 
docker tag boldreports-server-jobs:4.2.52_06042023_subha gcr.io/boldreports-dev/boldreports-server-jobs:4.2.52_unchain
 
 
docker tag boldreports-designer:4.2.52_06042023_subha gcr.io/boldreports-dev/boldreports-designer:4.2.52_unchain 
 
 
 
IDP  (PUSH IMG TO GCR )	
 
docker push gcr.io/boldreports-dev/bold-identity:4.2.52_unchain
 
 
docker push gcr.io/boldreports-dev/bold-idp-api:4.2.52_unchain 
 
 
docker push gcr.io/boldreports-dev/bold-ums:4.2.52_unchain 
 
 
Report Server 
 
docker push gcr.io/boldreports-dev/boldreports-server:4.2.52_unchain 
 
 
docker push gcr.io/boldreports-dev/boldreports-server-api:4.2.52_unchain 
 
 
docker push gcr.io/boldreports-dev/boldreports-server-jobs:4.2.52_unchain
 
 
docker push gcr.io/boldreports-dev/boldreports-designer:4.2.52_unchain 


___________________________________________________________________________________________


aws eks --region us-east-1 update-kubeconfig --name cluster57364 

helm install boldreports2 boldreports/boldreports -f values.yaml -n bold-services --create-namespace



helm package mychart --version 5.4 --app-version 5.3.8

helm repo add boldreports https://subasri-viswanathan.github.io/boldreports-helm/

C:\Users\SubasriViswanathan>helm repo list

helm upgrade boldreports boldreports -f values.yaml -n bold-services

kubectl create secret tls boldreports-tls -n bold-services --key "D:/cert/private-key.pem" --cert "D:/cert/certificate.pem" 

kubectl create secret tls boldreports-tls -n bold-services --key "private-key.pem" --cert "certificate.pem"

helm uninstall boldreports boldreports -n bold-services

helm install boldreports2 boldreports -f values.yaml -n bold-services

kubectl describe pod reports-api-deployment-fc4cdfd57-z9drr -n bold-services - To describe

Kubectl exec -it id-web-deployment-7cff6f5f5b-cpn77  -n bold-services -- bash  - To bash

kubectl get deploy -o wide -n bold-services -> get image

kubectl delete pod reports-web-deployment-6c8b7b4f5-75sm4 -n bold-services - To delete pod

kubectl delete pod reports-web-deployment-6c8b7b4f5-75sm4 -n bold-services --grace-period=0 --force  - To delete the pod immediately without waiting for grace period.

kubectl logs id-api-deployment-766dbb944b-rg5bq -n bold-services  -> To get pod logs 

kubectl get node -o wide -n bold-services 

kubectl delete ns bold-services -> To delete namespace 

kubectl create namespace my-namespace

_________________________________________________________________

kubectl rollout restart deployment/id-web-deployment -n bold-services2

kubectl rollout restart deployment/id-api-deployment -n bold-services2
kubectl rollout restart deployment/id-ums-deployment -n bold-services2
kubectl rollout restart deployment/reports-api-deployment -n bold-services2
kubectl rollout restart deployment/reports-jobs-deployment -n bold-services2
kubectl rollout restart deployment/reports-web-deployment -n bold-services2
kubectl rollout restart deployment/reports-reportservice-deployment -n bold-services2
kubectl rollout restart deployment/reports-viewer-deployment -n bold-services2

___________________________________________________________________________

Node Count: 5,

Instance type: --node-type c5d.xlarge

Cluster cost : 0.10USD/per hour
_____________________________________________________________________________	
To install BR using helm alb -ingress EKS

curl -o iam-policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.2.1/docs/install/iam_policy.json
kubectl apply -k "github.com/kubernetes-sigs/aws-efs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.4"

helm repo add boldreports https://subasri-viswanathan.github.io/boldreports-helm/
kubectl apply -k "github.com/aws/eks-charts/stable/aws-load-balancer-controller//crds?ref=master"
helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=cluster57364

helm install boldreports boldreports/boldreports -f eks-alb-values.yaml -n bold-services --create-namespace
kubectl create secret tls bold-tls -n bold-services --key "private-key.pem" --cert "certificate.pem"
kubectl get ingress -n bold-services
helm uninstall boldreports boldreports/boldreports -n bold-services

helm install boldreports boldreports/boldreports -f aks-values.yaml -n bold-services --create-namespace
helm upgrade boldreports boldreports -f aks-values.yaml -n bold-services



helm repo remove boldreports - To remove the repos
helm search repo - To get all charts
helm repo list - To get repo list

helm package boldreports - To pack the boldreports folder into tgz file.
helm package KC269938
helm package mychart --version 5.4 --app-version 5.3.8

Get-FileHash -Path .\boldreports-5.4.20.tgz -Algorithm SHA256 - To get digest valuse 
helm rollback - presivous version

https://subasri-viswanathan.github.io/boldreports-helm/boldreports-5.4.20.tgz - raw file

Ingress - helm chart.

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.7.0/deploy/static/provider/cloud/deploy.yaml

kubectl get svc -n ingress-nginx

helm repo add boldreports https://subasri-viswanathan.github.io/boldreports-helm/
___________________________________________________________

HELM FILE SYNTAX TEST:

 yamllint deployment.yaml
 helm lint 
 
___________________________________________

Helm using ISTIO: 

istioctl install

kubectl get svc -n istio-system
kubectl get pods -n istio-system
kubectl rollout restart deployment -n istio-system
kubectl describe pod istiod-ffb4844fd-pnt4b  -n istio-system

kubectl create secret tls bold-tls -n istio-system --key "private-key.pem" --cert "certificate.pem"

kubectl get gateway -n bold-services
kubectl get vs -n bold-services

helm repo remove boldreports
 
 
 To get k8's pplication logs,
 
 kubectl cp <namespace>/<pod_name>:<path_to_file_within_pod> </local/path/on/your/machine>

 kubectl cp bold-services/reports-api-deployment-844576f48d-qgvbf:/application/my-folder.tar.gz D://cert
 kubectl cp bold-services/reports-api-deployment-844576f48d-qgvbf:/application/app_data/logs D://cert/logs


Download file from Cluster

------------------------------------

apt-get update

apt-get install zip

apt-get install curl

To zip the folder run the following

----------------------------------------------

zip -r my_folder.zip . or tar -czvf my-folder.tar.gz app_data

curl bashupload.com -T logs.zip

you can get the download link

_________________________________________________

istioctl version
kubectl -n istio-system get deployment istiod
kubectl -n istio-system get deployment istio-ingressgateway

client version: 1.18.3
control plane version: 1.18.3
data plane version: 1.18.3 (1 proxies)

kubectl top nodes - To check memory

kubectl config current-context

helm list --all-namespaces

helm list -n bold-services

helm uninstall boldreports boldreports/boldreports - uninstall

--------------------------------------
