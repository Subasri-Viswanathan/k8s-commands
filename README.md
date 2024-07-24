# k8s-commands
Basic commands for k8s

Build Image
DP
docker build -t bold-identity:6.1.34_07242024_schedule -f bold-identity.txt .
docker build -t bold-idp-api:6.1.34_07242024_schedule -f bold-idp-api.txt .
docker build -t bold-ums:6.1.34_07242024_schedule -f bold-ums.txt .
 
Report Server
 
docker build -t boldreports-server:test -f boldreports-server.txt .
docker build -t boldreports-server-api:test -f boldreports-server-api.txt .
docker build -t boldreports-server-jobs:test -f boldreports-server-jobs.txt .
docker build -t boldreports-designer:test -f boldreports-designer.txt .
docker build -t boldreports-viewer:test -f boldreports-server-viewer.txt .
docker build -t bold-etl:test -f bold-etl.txt .
 
 
 
docker tag bold-identity:6.1.45_06192024_releasetesting2 us-docker.pkg.dev/boldreports-dev/images/bold-identity:6.1.45_06192024_releasetesting2
docker tag bold-idp-api:test us-docker.pkg.dev/boldreports-dev/images/bold-idp-api:6.1.45_06192024_releasetesting
docker tag bold-ums:test us-docker.pkg.dev/boldreports-dev/images/bold-ums:6.1.45_06192024_releasetesting
 
docker tag boldreports-server:test us-docker.pkg.dev/boldreports-dev/images/boldreports-server:6.1.45_06192024_releasetesting
docker tag boldreports-server-api:test us-docker.pkg.dev/boldreports-dev/images/boldreports-server-api:6.1.45_06192024_releasetesting
docker tag boldreports-server-jobs:test us-docker.pkg.dev/boldreports-dev/images/boldreports-server-jobs:6.1.45_06192024_releasetesting
docker tag boldreports-designer:test us-docker.pkg.dev/boldreports-dev/images/boldreports-designer:6.1.45_06192024_releasetesting
docker tag boldreports-viewer:test us-docker.pkg.dev/boldreports-dev/images/boldreports-viewer:6.1.45_06192024_releasetesting
docker tag bold-etl:test us-docker.pkg.dev/boldreports-dev/images/bold-etl:6.1.45_06192024_releasetesting
 
 
Google Cloud:
IDP
docker push us-docker.pkg.dev/boldreports-dev/images/bold-identity:6.1.45_06192024_releasetesting2
docker push us-docker.pkg.dev/boldreports-dev/images/bold-idp-api:6.1.45_06192024_releasetesting
docker push us-docker.pkg.dev/boldreports-dev/images/bold-ums:6.1.45_06192024_releasetesting
 
 
Report Server
 
docker push us-docker.pkg.dev/boldreports-dev/images/boldreports-server:6.1.45_06192024_releasetesting
docker push us-docker.pkg.dev/boldreports-dev/images/boldreports-server-api:6.1.45_06192024_releasetesting
docker push us-docker.pkg.dev/boldreports-dev/images/boldreports-server-jobs:6.1.45_06192024_releasetesting
docker push us-docker.pkg.dev/boldreports-dev/images/boldreports-designer:6.1.45_06192024_releasetesting
docker push us-docker.pkg.dev/boldreports-dev/images/boldreports-viewer:6.1.45_06192024_releasetesting
docker push us-docker.pkg.dev/boldreports-dev/images/bold-etl:6.1.45_06192024_releasetesting

___________________________________________________________________________________________
To Apply Image:

kubectl set image deployment/id-web-deployment id-web-container=us-docker.pkg.dev/boldreports-dev/images/bold-identity:6.1.34_24072024_schedule --namespace=bold-services --record
 
kubectl set image deployment/id-api-deployment id-api-container=us-docker.pkg.dev/boldreports-dev/images/bold-idp-api:6.1.34_24072024_schedule --namespace=bold-services --record
 
kubectl set image deployment/id-ums-deployment id-ums-container=us-docker.pkg.dev/boldreports-dev/images/bold-ums:6.1.34_24072024_schedule --namespace=bold-services --record
 
kubectl set image deployment/reports-web-deployment reports-web-container=us-docker.pkg.dev/boldreports-dev/images/boldreports-server:6.1.34_24072024_schedule --namespace=bold-services --record
 
kubectl set image deployment/reports-api-deployment reports-api-container=us-docker.pkg.dev/boldreports-dev/images/boldreports-server-api:6.1.34_24072024_schedule --namespace=bold-services --record
 
kubectl set image deployment/reports-jobs-deployment reports-jobs-container=us-docker.pkg.dev/boldreports-dev/images/boldreports-server-jobs:6.1.34_24072024_schedule --namespace=bold-services --record
 
kubectl set image deployment/reports-reportservice-deployment reports-reportservice-container=us-docker.pkg.dev/boldreports-dev/images/boldreports-designer:6.1.34_24072024_schedule --namespace=bold-services --record
 
kubectl set image deployment/reports-viewer-deployment reports-viewer-container=us-docker.pkg.dev/boldreports-dev/images/boldreports-viewer:6.1.34_24072024_schedule --namespace=bold-services --record
 
kubectl set image deployment/bold-etl-deployment bold-etl-container=us-docker.pkg.dev/boldreports-dev/images/bold-etl:6.1.34_24072024_schedule --namespace=bold-services --record


_______________________________________________________________________________________________

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


_______________________________________________________________________________

kubectl describe pod reports-api-deployment-fc4cdfd57-z9drr -n bold-services - To describe

Kubectl exec -it id-web-deployment-7cff6f5f5b-cpn77  -n bold-services -- bash  - To bash

kubectl get deploy -o wide -n bold-services -> get image

kubectl delete pod reports-web-deployment-6c8b7b4f5-75sm4 -n bold-services - To delete pod

kubectl delete pod reports-web-deployment-6c8b7b4f5-75sm4 -n bold-services --grace-period=0 --force  - To delete the pod immediately without waiting for grace period.

kubectl logs id-api-deployment-766dbb944b-rg5bq -n bold-services  -> To get pod logs 

delete file inside the container: kubectl exec -n bold-services id-web-deployment-5b44f57976-7mz87 -- sh -c 'rm -rf /application/app_data/reporting/Jobs/Export/*'

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
