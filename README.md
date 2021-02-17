# Dokku-NodeJs-Sample-App
### Deployment of a Node.js project on AWS EC2 instance
##### This is just a static website hosting using NodeJs with express framework - images are hyperlinked.

### Update the Ec2 instance - Run the below commands as a root user 
```
apt-get update -y
```
### Bootstrap the node first
### for debian systems, installs dokku via apt-get
```
  wget https://raw.githubusercontent.com/dokku/dokku/v0.23.5/bootstrap.sh

  sudo DOKKU_TAG=v0.23.5 bash bootstrap.sh
```
 ### go to your server's IP and follow the web installer

### then enable the SSH key-based authentication
vim ~/.ssh/config
```
Host dokku
    HostName 54.xx.xx.xxx
    User ubuntu
    Port 22
    IdentityFile /dxx/xx/xxx-Key.pem
```
### login to the server and create a dokku app
```
dokku apps:create nodejs-sample-app

```

### Then you can deploy code from the dev system by initiating the git push
```
 git remote add dokku dokku@dokku:nodejs-sample-app

```
 #### after the git remote add (dokku - is the git remote name)
 #### dokku is the linux user for application life cycle maintenence
 #### @dokku - is the server name - where you've configured in ssh/config
 #### nodejs-sample-ap - is your dokku application name 
 
### Deploy the app
 ```
 git add .
 git commit -am "adding nodejs application to dokku"
 git push dokku master
 ```
 ``
=====> Application deployed:
To dokku:nodejs-sample-app
   8f923f2..e344afb  master -> master
   
``
### Map the DNS record to point to your EC2 instance static Public IP or Application Loadbalancer.

# test the app:
   @https://hello-world.cloudreinforce.com/
