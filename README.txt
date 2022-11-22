# Capstone--Project
 
# In this project i tried to implement DevOps lifecycle and deploy the code to the production 
For this project i needed three server one is master of ansible as well as jenkins and other two are slaves for the same.
one slave is named as test and other is named as prod.
Thus 3 servers are created through AWS and installed ansible on master and python3 on slave.
Slaves are connected to master by doing the required configuration.
Now playbook has been creatend for deploying docker and java on slaves and jenkins on master , shell scripting is used for doing the same.
Thus using ansible as a confuguration management tool we have deployed all the necessory softwares on slaves as well as on master.
git reporitory is created by the name of Capstone-Project.
required code is generated on master and develop branch has been created and pushed to github repository.
As jenkins has been succesfully installed on master we logged in to jenkins account and nodes have been connected.
New freestyle project with a name of "test" has been created.
This project is restricetd to test node only and in source code management github link is provided.
Also github hoot trigger for GITscm is marked and to work that trigger we have to create webhook trigger in respective git hub repository.
