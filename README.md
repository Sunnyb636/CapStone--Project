# Capstone--Project
 
# In this project i tried to implement DevOps lifecycle and deploy the code to the production 

For this project i needed three server one is master of ansible as well as jenkins and other two are slaves for the same.
one slave is named as test and other is named as prod.

Thus 3 servers are created through AWS and installed ansible on master and python3 on slaves.
Slaves are connected to master by doing the required configuration.

Now playbook has been creatend for deploying docker and java on slaves and jenkins on master , shell scripting is used for doing the same.
Thus using ansible as a confuguration management tool we have deployed all the necessory softwares on slaves as well as on master.

git reporitory is created by the name of Capstone--Project.
Required code is generated on master and develop branch has been created and pushed to github repository.

As jenkins has been succesfully installed on master we logged in to jenkins account and nodes have been connected.

New freestyle project with a name of "test" has been created.
This project is restricetd to test node only on develop branch and in source code management github link is provided.
Also github hook trigger for GITscm is marked and to work that trigger we have to create webhook trigger in respective git hub repository.

In execute shell commands used are as follow :
  sudo docker build <path of job> -t <name of job>
  sudo docker run -itd -p <port to be used :80> --name <name to be given> <name of job>
afetr first build shell commands are changed as follows: 
  sudo docker rm -f <name of job>
  sudo docker build <path of job> -t <name of job>
  sudo docker run -itd -p <port to be used :80> --name <name to be given> <name of job>
Thus 1st job is built properly and testing of code is done 

now again to test this code on master branch job-2 is created 
-this job is also restricted to test node but on master branch 
git hub link provided in SCM
same commands are used in this job to test if the code is working fine on master branch 
all looks good thus we are ready to push the code to production

file job-3 has been created in jenkins to deploy code in production
this time job is restricted to prod node and on master branch 
all the steps followed are same of the above jobs

Now as the code is deployed in production and is working fine , we need to create a pipeline such that job-3 will trigger only if job-2 is built successfully
for this requirement job-3 is configured again and markerd build trigger such that job-3 will only be triggered after the successfull built of job-2
Thus because of this pipeline - code will only get pushed to the production after the successfull testing of code on test servers 
                                                 *** Project is Completed ***
 
 #$ content used $ 🔽
 #playbook -
 ---
 - hosts: localhost
   name: master tasks
   become: yes
   tasks:
    - name: executing master
      script: master.sh
 - hosts: slave
   name: slave tasks
   become: yes
   tasks:
    - name: executing slaves
      script: slave.sh
 
#shell scripts 
master.sh:- 
sudo apt install docker.io -y
sudo apt install openjdk-11-jdk -y
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ >  /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins -y

slave.sh :- 
sudo apt install docker.io -y
sudo apt install openjdk-11-jdk -y
 
#dockerfile :- 
FROM ubuntu
RUN apt-get update
RUN apt install apache2 -y
ADD . /var/www/html
ENTRYPOINT apachectl -D FOREGROUND
 
#index.html file :- 
 
<html>
<head>
<title> Capstone-Project </title>
</head>
<body style = "background-image:url('devop.jfif'); background-size: 100%">
<h2 ALIGN=LEFT>Welcome to the world of magic!</h2>
</body>
</html>
