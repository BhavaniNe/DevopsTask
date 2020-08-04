# Kubernetes Cluster 
Install kubernates 

Need to do in both master and node
    # sudo passwd user
	# sudo passwd root
	 # vi /etc/ssh/sshd_config =====change password authentication to yes
    # hostnamectel set-hostname worker-node-1
     # hostnamectl set-hostname worker-node-1
      # service sshd restart
      #service sshd stop
     # service sshd start
     -- 
    # cat <<EOF>> /etc/hosts
      172.31.37.189 master-node
      172.31.35.99  worker node-1
     EOF
	 ----
    # setenforce 0
    # sed -i --follow-symlinks 's/SELINUX=enforcing/SENUX=pedisabled/g' /etc/sysconfig/selinux
    #  reboot
    # yum-config-manager --disable kubernetes
	 -----
   # cat <<EOF > /etc/yum.repos.d/kubernetes.repo
     [kubernetes]
     name=Kubernetes
     baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
     enabled=1
     gpgcheck=1
     repo_gpgcheck=1
     gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
     EOF
  ------
    # yum-config-manager --save -setopt-kubernetes.skip_if_unavailable=true
    # yum install kubeadm docker -y
    # yum install -y kubelet kubeadm kubectl
    # yum install -y kubelet kubeadm kubectl --disableexcludes=kubernates
    # systemctl enable kubelet
    # systemctl start kubelet
    # systemctl enable docker
    # systemctl start docker
  
Untill here need to do for both master and nodes

This bellow command is done only for master ...
                                           {{ ipv of instance }}
# kubeadm init --apiserver-advertise-address=172.31.37.189 --pod-network-cidr=192.168.1.1/16  --ignore-preflight-errors=NumCPU

Copy the token displayed after exicution of above command and place in node . then cluster nodes will be created

Go back to master the make a dir of kubead
     # mkdir -p $HOME/.kube    #####  no need root prompt now cause this give full permission to user
     # sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
	 # sudo chown $(id -u):$(id -g) $HOME/.kube/config
	 # kubectl get nodes
:~   # kubectl get pods --all-namespaces
	 # export kubever=$(kubectl version | base64 | tr -d '\n')
:~   # kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$kubever"
==================== you have a succesfully turned up a kubernetes cluster=======================



  # kubectl create deployment --image nginx nginxdemos
  # kubectl get pods
  # kubectl get deployment 
  # kubectl scale deployment --replicas 2 nginxdemos
  # kubectl get services    ### going to say the internal Ip and inginx web server is 443##
  # kubectl get pods
  to delete the pods
  # kubectl delete deployment nginxdemos
	creat an Yaml file 
	-----
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-hello-world
spec:
   selector:
      matchLabels:
        app: nginx
   replicas: 3
   template:
      metadata:
        labels:
         app : nginx
      spec:
        containers:
          - name: nginx
            image: nginx:1.14.2
            ports:
             - containerPort: 80

	
	
	
	
	----
	
	# kubectl create -f deploy.yaml
	# kubectl get po
	# kubectl get po -o wide
	
	
	Get back to the worker node
	# sudo docker ps
	
	============== go back to master node ========
	# kubectl create service nodeport nginx --tcp=80:80
	# kubectl get svc
	///* now public ip of master aws instances and type port in browser///



