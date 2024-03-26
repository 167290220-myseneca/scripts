# scripts

 Assignment 2
  
  
  
  scp -i key-dev init_kind.sh kind.yaml mysqlpod.yaml pod-web.yaml 3.85.135.148:/tmp
  
  
  
  kubectl create -f mysqlpod.yaml
  kubectl get pods
  kubectl get pod assignment2-mysql -o wide
  
  kubectl create -f pod-web.yaml
  
  scp -i key-dev app-deployment.yaml assig2-mysql-replicaset.yaml assign2-webapp-replicaset.yaml sql-deployment.yaml 54.237.145.29:/tmp
  
   kubectl port-forward pod/assignment2app 8080:8080 
   scp -i key-dev assignment2-app-service.yaml assignment2-mysql-service.yaml 44.201.139.233:/tmp
     
   -always mysql first   


  kind delete cluster
  
  namespace :
  kubectl create ns sql
  kubectl create ns app
  kubectl get ns
  
  
  kubectl create -f mysqlpod.yaml -n sql
  kubectl get pod assignment2-mysql -o wide -n sql
  kubectl get pods -n sql
  
   the file check ip address of pod.yaml change ip address
   exit scp
   
  ssh
  
  kubectl create -f pod-web.yaml -n app 
  kubectl get pods -n app
  
  port forwarding:
  kubectl port-forward pod/assignment2app -n app 8080:8080

  new terminal ssh
  curl localhost:8080
  
  replicaset:
  kubectl create -f assig2-mysql-replicaset.yaml -n sql
  kubectl get pods -n assignment2sql
  kubectl create -f assign2-webapp-replicaset.yaml -n app
  kubectl get pods -n assignment2app
   
   note to delete we use  
   - kubectl delete  pod assignment2-mysql-replicaset-svhxn -n assignment2app
   
   deployment:
   kubectl create -f sql-deployment.yaml -n sql
   kubectl get pods -n assignment2sql
   kubectl create -f app-deployment.yaml -n app
   kubectl get pods -n assignment2app
   
   service:
    kubectl create -f assignment2-mysql-service.yaml -n sql
    kubectl get pods -n assignment2sql 
    kubectl create -f assignment2-app-service.yaml -n app
    kubectl get pods -n assignment2app
    
    note :
    check instance tcp 30000 inbound rule
    http://44.201.139.233:30000/
    
 note for report : [ec2-user@ip-172-31-82-189 tmp]$ kubectl cluster-info
Kubernetes control plane is running at https://127.0.0.1:46429
KubeDNS is running at https://127.0.0.1:46429/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
[ec2-user@ip-172-31-82-189 tmp]$ 


change the version and color of app-deployment.yaml 
kubectl apply -f app-deployment.yaml -n app
http://44.201.139.233:30000/

in c9
  
 curl http://44.201.139.233:30000/
  
  
  Assignment1
  
  ssh -i keyname IP

sudo yum update -y  sudo yum install docker -y sudo systemctl start docker sudo systemctl status docker

-sudo usermod -aG docker ec2-user logout sudo systemctl start docker

aws configure vi ~/.aws/credentials Giving all the AWS credentials push commands login successful

-docker pull image db URI -docker pull image app -docker images

-docker network create -d bridge test

docker run -d --network=test -e MYSQL_ROOT_PASSWORD=pw url of app export DBHOST=172.18.0.2 export DBPORT=3306 export DBUSER=root export DATABASE=employees export DBPWD=pw export APP_COLOR=blue

docker run -p 8081:8080 --name blue -e DBHOST=$DBHOST -e DBPORT=$DBPORT -e DBUSER=$DBUSER -e DBPWD=$DBPWD -e APP_COLOR=blue --network=test url of db_image -docker ps We need to go inside one of the containers with this cmd: -docker exec -it <blue/pink/lime> /bin/bash And then install ping in that container using:

-apt-get update -apt-get install iputils-ping

-ping pink(The other container's name)

Extra commands
Stop all running containers
docker stop $(docker ps -q)
