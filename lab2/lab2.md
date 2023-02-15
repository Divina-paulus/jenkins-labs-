## lab2

1-configure jenkins image to run docker commands on your hos docker daemon
```
touch Dockerfil
vi Dockerfile
```
<img src="https://user-images.githubusercontent.com/92440274/217831255-4a019a2f-70c6-4ce8-8a11-8cd518587f5f.png">

```
docker image build . -t jenkins-docker

docker run -it -d -p 8083:8080 -p 50000:50000 -v /var/run/docker.sock:/var/run/docker.sock -v jenkins_home:/var/jenkins_home jenkins-docker

```
```
docker ps
```
```
docker exec -it 4afcf4732320 bash
```
```
docker ps
```
<img src="https://user-images.githubusercontent.com/92440274/217833592-5d9fcbca-ba14-4eef-afbc-dc7d51de2be6.png">

2- create CI/CD for this repo https://github.com/mahmoud254/jenkins_nodejs_example.git.

<img src="https://user-images.githubusercontent.com/92440274/218078314-5d2750c1-2f2e-46f5-865c-27fcaa80fef7.png">

<img src="https://user-images.githubusercontent.com/92440274/218078665-66680cf6-4251-45fb-837f-39cf605409b5.png">

<img src="https://user-images.githubusercontent.com/92440274/218078878-c7412e83-130c-4bab-be58-bbed689a0930.png">

<img src="https://user-images.githubusercontent.com/92440274/218080613-17c08b8e-39ac-4ba6-9c5a-eaae738466ed.png">

<img src="https://user-images.githubusercontent.com/92440274/218080815-b39e3c8a-1077-45fa-92d3-92584446ccea.png">

#############################################################
1- create docker file to build image for jenkins slave
```
FROM ubuntu

USER root

RUN mkdir -p jenkins_home
RUN chmod 777 jenkins_home

ENV DEBIAN_FRONTEND noninteractive
ENV TZ=Africa/Cairo

RUN apt-get update

RUN apt-get install -y tzdata

RUN apt-get install -y openjdk-11-jdk

RUN apt-get install -y openssh-server


# Install dependencies required to install Docker
RUN apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common

# Add the Docker GPG key
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

# Add the Docker repository
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Update the package repository again
RUN apt-get update

# Install Docker
RUN apt-get install -y docker-ce docker-ce-cli containerd.io

# Verify the Docker installation
RUN docker --version

RUN useradd -ms /bin/bash jenkins
RUN usermod -aG docker jenkins

WORKDIR jenkins_home

CMD [ "/bin/bash" ]
```
```
docker build -t jenkins-slave-image:v1 .
```
<img src="https://user-images.githubusercontent.com/92440274/218130804-6983b4e3-b0b6-4f96-ac27-c65dbd401ee0.png">

2- create container from this image and configure ssh

```
docker run -it -d --name jenkins-slave-cont jenkins-slave-image:v1
docker ps
docker exec -it b7e6ba92a695 bash

```
```
ssh-keygen
cd /root/.ssh
ls
cp id_rsa.pub authorized-keys
```
<img src="https://user-images.githubusercontent.com/92440274/218141938-c79272e4-9352-484b-b585-6d892b949258.png">

3-from jenkins master create new node with the slave container

<img src="https://user-images.githubusercontent.com/92440274/218918484-4d2f1981-e31b-4373-9f0c-adc9b6971e9d.png">

<img src="https://user-images.githubusercontent.com/92440274/218918504-97014b51-b637-424d-8a96-47ed21b4f85a.png">


4- integrate slack with jenkins

<img src="https://user-images.githubusercontent.com/92440274/219002481-c4e7a6df-6977-4796-9080-456c896078f9.png">

<img src="https://user-images.githubusercontent.com/92440274/219002500-9382a515-f663-43de-8467-3133eb398169.png">

5- send slack message when stage in your pipeline is successful
```
post {
    success {
        slackSend color: 'good', message: "Build succeeded! Visit ${env.BUILD_URL}"
    }
    failure {
        slackSend color: 'danger', message: "Build failed! Check the logs at ${env.BUILD_URL}"
    }
}
```
<img src="https://user-images.githubusercontent.com/92440274/219022765-e5cc3382-431e-44d3-b399-0a3168049da6.png">

<img src="https://user-images.githubusercontent.com/92440274/219023085-00b77fe1-dfe9-4db9-80de-1bea82e2b9a8.png">

6- install audit logs plugin and test it
<img src="https://user-images.githubusercontent.com/92440274/219030583-5b0c22ed-a081-45c7-b134-a00965d6ee11.png">

- Build Now to any pipeline
- choose manage jenkins, then choose manage plugins and audit log plugin
<img src="https://user-images.githubusercontent.com/92440274/219031321-6da62a82-e856-4ce1-ab79-af997d47b095.png">


7- fork the following repo https://github.com/mahmoud254/Booster_CI_CD_Project and add
dockerfile to run this django app and use github actions to build the docker image and push it to
your dockerhub
Create infrastructure pipeline to run terraform with jenkins
task
Create ansible script to configure application ec2(private)

