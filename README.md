ansible-playbooks
=================

Sample [Ansible](http://www.ansibleworks.com/) Playbook for [Django](https://www.djangoproject.com) that installs Nginx, Passenger, and Django 1.6.  It also demonstrates how to deploy a sample Django "Hello World" application.

 Specifically, it does the following:

 * Updates the OS and Installs a few common packages like NTP and VIM
 * Creates a deploy user that the application files will belong to
 * Adds an SSH public key to the deploy user's Authorized Keys file
 * Reconfigures OpenSSH to only allow access via SSH keys
 * Installs Django 1.6 for use with Python 2.7 or 3 
 * Installs Ruby 1.9.3 (For installing Passenger Gem)
 * Installs Nginx + Passenger
 * Sets up and enables an Nginx vhost
 * Creates all necessary application directories and files to create a Django Hello World application.


Running this playbook will leave you with a fully-functional Django server that leverages Nginx and Phusion Passenger as well as displaying a hello world application. This will allow you to create your own Django application using Python 2.7 or 3 (Currently the App is running using python 2.7). 

This playbook was tested on Ubuntu 12.04.2 LTS but should run on Debian. 

Running the Playbook on Ubuntu
----------------------------------

* Install [Ansible](http://www.ansibleworks.com/docs/intro_installation.html). This playbook requires version >1.4, which  means you need the development version.
* Add your Hosts IP to `inventories/django_app`
* Modify the `vars/nginx-django` as needed
* Replace `roles/deploy-user/files/id_rsa.pub` with your public key
* When the Ansible provisioning completes, visit http://yourip.com


Running the Playbook with Vagrant
----------------------------------
* Install [Vagrant](http://downloads.vagrantup.com)
* If using Vmware with Vagrant you will need to puchase both Vmware and the Vagrant Plugin(I personally have done this). The Vagrant file in my repo expects this. 
* If you want to use Vagrant with Virtualbox please read the documentation [here](http://docs.vagrantup.com/v2/getting-started/index.html). You will also need to Modify the Vagrant file located in the root directory to look something like [this](http://docs.vagrantup.com/v2/provisioning/ansible.html). Please see jlund's example Vagrant file [here](https://github.com/jlund/mazer-rackham) 
* Once you have your chosen set up, run `vagrant up` this will run the vagrant.yml 
* You may then run the nginx-django.yml against your Vagrant environemnt by running the following command: `ansible-playbook -i inventories/vagrant nginx-django.yml`
* View the app at `http://localhost:8080` (or whatever port you chose to forward via the Vagrant file)
 
Important Info
----------------------------------
* Note that debugging is enabled by default when a Django app is created. If you plan on keeping the example app, I suggest that you turn off debugging by modifying the settings.py located in the application directory. 

Future Enhancements 
----------------------------------
* I would like to implement this using a [virtualenv](http://www.virtualenv.org/en/latest/)

Credit
----------------------------------
* I based part of this playbook off of [mazer-rackham](https://github.com/jlund/mazer-rackham) written by jlund. I would like to personally thank jlund for his work, he has been a good friend and `*nix` mentor
