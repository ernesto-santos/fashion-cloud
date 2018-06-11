# 1) Environment setup:

## 1.1) Install Ansible:

Ansible Install Guide:

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

1.5) Go to the directory where your cloned repository is:

$ cd ./fashion-cloud


1.6) Change the "Access Key ID" and "Secret Access Key" in the "set_credentials.sh" script:

$ cat set_credentials.sh
export AWS_ACCESS_KEY_ID='<<the_provided_access_key>>'
export AWS_SECRET_ACCESS_KEY='<<the_provided_secret_access>>'
export EC2_INI_PATH=./aws-invent/ec2.ini 


1.7) Run the script, to put the needed env vars in the shell memory:

$ . ./set_credentials.sh


1.8) Load the the private key to the ssh agent:

$ ssh-add ./key-pair/fashion-cloud.pem

$ # if you want to check.. 
$ ssh-add -l


2) Creating the AWS components:

Run the script to create the componentes:

$ ansible-playbook -i ./aws-invent/ec2.py ./fashion-cloud-playback_create.yml





$ ssh ubuntu@52.23.174.160 -i ./key-pair/fashion-cloud.pem





$ ansible-playbook -i ./aws-invent/ec2.py fashion-cloud-playback_cleanup.yml
