# 1) Environment setup:

## 1.1) Install Ansible:

https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

## 1.2) Install the Python Ansible module:

```
$ pip install ansible
```

## 1.3) Install the Python Boto modules:

```
$ pip install boto
$ pip install boto3
```

## 1.4) Clone the repository to your local machine:

```
$ git clone https://github.com/ernesto-santos/fashion-cloud.git
```

## 1.5) Go to the directory where your cloned repository is:

```
$ cd ./fashion-cloud
```

## 1.6) Change the "Access Key ID" and "Secret Access Key" in the "set_credentials.sh" script:

```
$ cat set_credentials.sh
export AWS_ACCESS_KEY_ID='<<the_provided_access_key>>'
export AWS_SECRET_ACCESS_KEY='<<the_provided_secret_access>>'
export EC2_INI_PATH=./aws-invent/ec2.ini 
```

## 1.7) Run the script, to put the needed env vars in the shell memory:

```
$ . ./set_credentials.sh
```

## 1.8) Load the the private key to the ssh agent:

```
$ ssh-add ./key-pair/fashion-cloud.pem

$ # if you would like to check the key.. 
$ ssh-add -l
```




# 2) Creating the AWS components:

Run the script to create the components:

```
$ ansible-playbook -i ./aws-invent/ec2.py ./fashion-cloud-playback_create.yml
```




# 3) The webservers IP addresses:

## 3.1) Showing the webservers instances info:

```
$ ansible-playbook -i ./aws-invent/ec2.py ./fashion-cloud-playback_show_instances.yml
```

# 3.2) Connecting to the instances, via ssh: 

```
$ ssh ubuntu@<<instance_name_or_ip>> -i ./key-pair/fashion-cloud.pem
```




# 4) The LB:

## 4.1) Showing the LB info (this will show you the URL to use on the web browser):

```
$ ansible-playbook -i ./aws-invent/ec2.py ./fashion-cloud-playback_show_lb.yml
```




# 5) If you want to change the nginx index.html content:

Edit the script "fashion-cloud-playback_update_webservers.yml".

Then execute it to update the instances.

```
$ ansible-playbook -i ./aws-invent/ec2.py ./fashion-cloud-playback_update_webservers.yml
```




# 6) When you finish, you can clean-up the env:

This script will remove all the created components.

OBS: Maybe you will need to execute the script twice, intending to remove the "security group". This is because it is dependency for the instances, and we need to remove/terminate the instances before we can remove the "security group".

```
$ ansible-playbook -i ./aws-invent/ec2.py ./fashion-cloud-playback_cleanup.yml
```




I hope you enjoy the lab / challenge.

Please, let me know if something does not work properly.



Best,

Ernesto 
