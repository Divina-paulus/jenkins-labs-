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



