#################################################################################################################
Host EKS CLUSTER via EKSCTL
#################################################################################################################
 create iam role and attach policy
 ECRfull access,EKSpolicy and IAM full access
 apt-get update -y
 apt install unzip -y
 curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
 unzip awscliv2.zip
 sudo ./aws/install
 aws configure
 Install EKS Tool
 curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
 sudo mv /tmp/eksctl /usr/local/bin
 eksctl version
 Install Kubectl
 curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
 sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl 
 kubectl version --client
 SSh-keygen
 Create EKS Cluster
 eksctl create cluster --name my-cluster --region region-code --version 1.32 --vpc-public-subnets subnet-ExampleID1,subnet-ExampleID2 --without-nodegroup
##############################################################################################################################
 ##Create a Node Group##
##############################################################################################################################
 eksctl create nodegroup \
  --cluster my-cluster \
  --region us-east-2 \
  --name my-node-group \
  --node-ami-family Ubuntu2204 \
  --node-type t2.small \
  --subnet-ids subnet-086ced1a84c94a342,subnet-01695faa5e0e61d97 \
  --nodes 3 \
  --nodes-min 2 \
  --nodes-max 4 \
  --ssh-access \
  --ssh-public-key /root/.ssh/id_rsa.pub







https://github.com/sanjayguruji/Sanjaya-K8S-Code/blob/main/Eks-cluster-creating
pods ->

mkdir /k8s-code

cd /k8s-code
vim mydeployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80

save and exit	
kubectl apply -f mydeployment.yaml
kubectl get deployment
deployment will be live


do this:
kubectl expose deployment nginx-deployment --port=80 --target-port --type=LoadBalancer


service code:

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer

kubectl apply -f service.yaml
