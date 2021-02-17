# Dokku-NodeJs-Sample-App
### Deployment of a Node.js project on AWS EC2 instance
##### This is just a static website hosting using NodeJs with express framework - images are hyperlinked.

### Update the Ec2 instance - Run the below commands as a root user 
```
apt-get update -y
```
### Bootstrap the node first - Run the following commands
#### for debian systems, installs dokku via apt-get

```
  wget https://raw.githubusercontent.com/dokku/dokku/v0.23.5/bootstrap.sh

  sudo DOKKU_TAG=v0.23.5 bash bootstrap.sh
```
### Now login to the ser and create a dokku app
```
dokku apps:create nodejs-sample-app

```

#### Once app is created verify the app created status by running the below command
```
 dokku apps:list
 ```
 
## Next enable the SSH key-based authentication from the development machine to make connectivity via hostname(Eg: dokku) and username and private key

vim ~/.ssh/config
```
Host dokku
    HostName 54.xx.xx.xxx
    User ubuntu
    Port 22
    IdentityFile /dxx/xx/xxx-Key.pem
```
### Run the below command from the source code directory. This will add the remote repository  
```
 git remote add dokku dokku@dokku:nodejs-sample-app

```
Notes: 
 #### after the git remote add (First `dokku` - is the git remote name)
 #### Second `dokku` is the linux user for application life cycle maintenence
 #### `@dokku` - is the server name - where you've configured in ssh/config
 #### `nodejs-sample-app` - is your dokku application name which created in the above step
 
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
