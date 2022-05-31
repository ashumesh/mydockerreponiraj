Jenkins Pipeline to create docker image and upload to ecr and create docker container from ECR
# mydockerrepo

1. Install Docker on jenkins server -> sudo apt install docker.io -y
2. give permision to docker -> sudo chmod 777 /var/run/docker.sock
3. install aws cli -> sudo apt install awscli
4. install docker and docker pipeline plugin in jenkins
5. install ssh pipeline plugin and gradle
