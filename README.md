# wordpress-mysql-k8s
This repo deals with deploying wordpress and mysql on k8s

## Minikube:
Steps to deploy the services:
1. First create secrets by running `kubectl apply -f secret.yml`.
2. Create mysql service,pvc and delployment by running `kubectl apply -f mysql.yml`. You can change the volume size based on your requirements. I have used `1G` for testing purpose.
3. Create wordpress service,pvc and deployment by running `kubectl apply -f wordpress.mysql`.
4. Now run the commands to check the resources:
  `kubectl get pvc && kubectl get pods && kubectl get svc`.
5. If you are running the above resources in minikube, then run `minikube service wordpressServiceName` to access the portal/frontend.
6. If you are running on any cloud based k8s service, Make sure the loadbalancer is created and accessible by exposing it to public.
7. If you want to change the secrets, replace the encoded value with your password. Cmd to encode is `echo -n 'my-string' | base64` and to decode `echo -n 'bXktc3RyaW5n' | base64 --decode`


## Cloud based:
1. Follow the same steps from 1-4.
2. Access the url from service, since we have selected the `LoadBalancer` type, it will give us url link through which we can access it.
3. Check the logs of both the pods by running `kubectl logs -f podName`.

Note:
1. Create cluster in GCP, using command `gcloud container clusters create hello-cluster --num-nodes=2`. This will create cluster called hello-cluster with 2 nodes, I have set default region as `us-central1-a` you can change it based on your requirements.
2. In previous commit the ClusterIP was none, for mysql service.That has been changed.
3. And new args has been added in mysql deployment to ignore `lost+found` dir as it throws the error, add the following below imagename under specs.
```
          args:
          - "--ignore-db-dir=lost+found"
```
4. Delete all the resources by running `kubectl delete -f wordpress.yml && kubectl delete -f mysql.yml && kubectl delete -f secrets.yml` and delete the cluster by running `gcloud container clusters delete hello-cluster` .
