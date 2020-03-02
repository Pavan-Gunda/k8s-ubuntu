# k8s-ubuntu

This repository has ansible scripts to create a kubernetes cluster in couple of minutes. 

Requirements: 
1 master node and any number of worker nodes that are connected to same network.

step1: 
clone the repo to your local(prefer this) or master host and install ansible.
add your master and worker hosts and their ip addresses to host file. 

step2:(optional) create a non root user with sudo permissions in order to ssh into them as a regular user, which lessens the risks of performing unintentional modifications. 

step3:To initiate the cluster, run the intial.yml file with no changes. 
ansible-playbook -i hosts ~/kube-cluster/initial.yml

step4:

run the dependencies playbook to install all the required configs and dependencies.
ansible-playbook -i hosts ~/kube-cluster/kube-dependencies.yml


step5:
change the cidr values to your cidr values and run the master.yml 

ansible-playbook -i hosts ~/kube-cluster/master.yml


step6:
join the worker nodes using the joinworkers.yml

ansible-playbook -i hosts ~/kube-cluster/joinworkers.yml


there could be an issue related to config files and there may be an errors that says 

 The connection to the server localhost:8080 was refused.

please run these commands as a regular user in order to rectify the error

sudo cp /etc/kubernetes/admin.conf $HOME/

sudo chown $(id -u):$(id -g) $HOME/admin.conf

export KUBECONFIG=$HOME/admin.conf
