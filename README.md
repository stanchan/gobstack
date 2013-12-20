openstack_demo
==============

Scripted openstack installation using Vagrant

***

######Requirements

* GNU/Linux host
* Virtualbox
* Vagrant

***

######Procedure

Running the script `./bootstrap.sh` will do this:

0. `you@host:~$ vagrant up`
0. `you@host:~$ vagrant ssh controller0`
0. On controller0:

    ``` 
    vagrant@controller0:~$ sudo /vagrant/installers/keystone.sh
    vagrant@controller0:~$ sudo /vagrant/installers/glance.sh
    vagrant@controller0:~$ sudo /vagrant/installers/nova_controller.sh
    vagrant@controller0:~$ sudo /vagrant/services/image_create.sh
    ``` 

0. Install swift on the storage node:
    `you@host:~$ vagrant ssh storage0 -c "sudo /vagrant/installers/swift.sh"`

0. Install nova on the compute nodes:
    `you@host:~$ for i in 0 1; do vagrant ssh compute$i -c "sudo /vagrant/installers/nova_compute.sh"; done`

***

######Use

Now you can boot an instance from controller0

`you@host:~$ vagrant ssh controller0 -c "/vagrant/services/instance_boot.sh"`

