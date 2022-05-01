# wordpress-mysql-k8s
This repo deals with deploying wordpress and mysql on k8s

Steps to deploy the services:
1. First create secrets by running `kubectl apply -f secret.yml`.
2. Create mysql service,pvc and delployment by running `kubectl apply -f mysql.yml`.
3. Create wordpress service,pvc and deployment by running `kubectl apply -f wordpress.mysql`.
4. Now run the commands to check the resources:
  `kubectl get pvc && kubectl get pods && kubectl get svc`.
5. If you are running the above resources in minikube, then run `minikube service wordpressServiceName` to access the portal/frontend.
6. If you are running on any cloud based k8s service, Make sure the loadbalancer is created and accessible by exposing it to public.
