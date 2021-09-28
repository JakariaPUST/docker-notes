# docker-notes

Docker Commands: [Commands](#Commands)


### Basic Queries ### 

1. [Why docker?](#Why-docker?)
2. [Why not virtual machines?](#Why-not-virtual-machines?)
3. [Is this Documentation enough?](#Is-this-Documentation-enough-for-docker?)

### **Why docker?** ###
Official answer is [ HERE](https://docs.docker.com/get-started/overview/#what-can-i-use-docker-for).
But in practically, 
- Docker is a platform for building, running, shipping applications in a consistent manner. It makes sure an application will work fine in other computers with different OS, different environments or different configuration settings even if the app is in development mode.
- For Docker different versions of the application will run side by side in the same machine.
- Docker mainly help us in production level, If any package version go backdated in our production running OS environment, then docker will come with images and containers, we can easily update the versions of the backdated packages in a new container without affecting production OS Configurations (without docker it's complicated), then active the container. If we mess something, then we can go back to the previous container easily. 
- If a new member joins our team, he doesn't need to install/configure all the dependencies in his machine.

### **Why not virtual machines?**  ###
Virtual machines are less efficient because they access the actual physical hardware resources. They are a little bit slower. On the other hand, Docker container image is a lightweight, standalone, executable package of software.  It starts quickly. It shares the OS of the host, that means we need to monitor only an operating system. Container doesn't need the physical resources of the host.

### **Is this Documentation enough for docker?** ### 
Almost all the practical docker Commands and Notes will be mentioned in this documentation. But if details are needed then go and explore Docker's official documentation.

See details Commands and Notes on Docker by Md. Jakaria.

### Commands:

1. Check docker installed or not 
```
docker --version
```
2. Docker Image list show:
```
docker image ls
```
3. Docker Container list show:
```
docker ps -a
```
4. Running docker container list:
```
docker ps
```
5. Remove all containers:
```
docker rm -vf $(docker ps -aq)
```
6. Remove all the images:
```
docker rmi -f $(docker images -aq)
```
7. Remove specific image:
```
docker rmi bf756fb1ae65
```
*NB=> {bf756fb1ae65 = image id}

8. Installing image in local from docker hub images:
```
docker pull ubuntu:latest
``` 
OR
```
docker image pull ubuntu:latest
```
*NB=> {ubuntu = image name, latest=version}
9. Installing specific image in local from docker hub images:
```
docker image pull ubuntu:18.04
```
10. Docker pull + start at once:
```
docker run redis:4.0
```
*NB=> {redis = image name, 4.0=version}
11. Start new container in detached mode:
```
docker run -d redis
```
*N.B=> redis is an image. (-d for Detached mode) it allows images to run in the same container id.It also gives access to use terminal again.
12. Restart Container:
```
Docker stop bf756fb1ae6
```
```
Docker start bf756fb1ae6
```
*N.B=>{bf756fb1ae6= container}.
13. Docker & Ports (run two different image version on same port but different host machine ports:
- Run:
```
docker ps -a
```
- If not showing containers then run in detached mode.
- Check the `docker ps -a` again. It will show details of containers.
- Say I have 2 different versions of redis. i) redis ii) redis:4.0 . 
  So we are going to run those two images on the same port 6379. 
- Run for the first one.
```
docker run -p6000:6379 -d redis
```
- Run for the Second one.
```
docker run -p6001:6379 -d redis:4.0
```
- Run `docker ps` . see the ports section ( two host port running on same docker container port)
14. Changing default name of an Image:
```
docker stop 6f5673788
```
NB->  6f5673788 is the name of the image.
[docker run -d -p6000:6379 --name redis-newname redis:4.0]
{redis-newname = new name what we are going to put} 
[docker ps] 
{now check the name of the image on the right side.} 

15. Docker run + start CMD difference:
[docker run] - it creates a new container. Also it will take an image with specific version or latest as an option or attribute.
[docker start] -it does not work with images, works with containers. Also it used to restart a container. 

16. Debugging & troubleshooting docker:
[docker ps]
[docker logs 6f5673788]
		NB.> {6f5673788=id of the image}
Get the running container for debugging:
[docker exec -it 6if5677654 /bin/bash] - entering into the corresponding container

After getting into the container try:
[ls, pwd, cd /, ls, env, exit] etc commands to see if the container goes correctly or not.
NB. > { ls = list showing, pwd= show the working directory, cd / = goes 1 step up, env= shows environment setup correctly, exit = exit from that container }.


Continue... 
