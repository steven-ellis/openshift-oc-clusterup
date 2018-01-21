
OpenShift OC Cluster Up
-----------------------

Simple playbook to pull in all dependancies for a RHEL client to run

	oc-cluster up

using the latest spins from OpenShift Origin

## Requirements
A vanilla base RHEL 7 or Centos 7 environment with
* 40GB+ Disk
* SELinux and Firewalld enabled

## Steps
Due to some issues with firewalld you need to create the dockerc zone before running the playbook

    firewall-cmd --permanent --new-zone dockerc
    firewall-cmd --reload

Then execute the ansible playbook with an appropriate host file

    ansible-playbook -i host main.yml


Once completed you have all the required dependancies for
* Docker
* Git
* oc-cluster

You can enable the environment under your user by typing

    cd 
    echo 'PATH=$HOME/oc-cluster-wrapper:$PATH' >> $HOME/.bash_profile
    echo 'export PATH' >> $HOME/.bash_profile
    . ./.bash_profile 

You can then use "oc-cluster" to run multiple OpenShift environments, including different releases
On my machine the public IP of my host is 192.168.122.157 so I'd run the following

    oc-cluster up example --public-hostname=192.168.122.157


## References
* https://github.com/openshift-evangelists/oc-cluster-wrapper
* https://developers.redhat.com/blog/2017/02/23/openshift-for-developers-set-up-a-full-cluster-in-under-30-minutes/
* https://wiki.centos.org/SpecialInterestGroup/PaaS/OpenShift-Quickstart 
* https://github.com/openshift/origin/blob/master/docs/cluster_up_down.md#linux

