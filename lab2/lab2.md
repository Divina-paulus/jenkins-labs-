#lab2

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

