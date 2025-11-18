#  EKS Cluster (Elastic Kubernetes Service)

## 1. Create EKS Cluster

. Create IAM Role 

. Security Group

.  Create EKS Cluster

## 2. EC2 (Elastic Compute Cloud) -

. Launch instance 

. Instance Type - (Big)

. Storage - (20 GB)

. Launch instance 

. Connect



### 1. Switch to root user
```sh
sudo -i
```


### 2. Update the instance
```sh
apt update
```

### 3. Install kubectl :  Download the latest release with the command
```sh
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

#### Validate the binary
```sh
 curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
```

#### Validate the kubectl binary against the checksum file 
```sh
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```

#### Install kubectl
```sh
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

#### Note: If you do not have root access on the target system, you can still install kubectl to the ~/.local/bin directory:
```sh
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
```
```sh
kubectl version --client
```

### 4. Install AWS CLI on Ubuntu

#### Download the aws cli bundle using below command
```sh
sudo apt install unzip -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

### 5. Configure AWS CLI

#### To connect AWS using CLI we have configure AWS user using below command
```sh
aws configure
```

## 3. EKS Cluster 

. Cluster Select

. Cluster Node
