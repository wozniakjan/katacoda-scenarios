## Docker introduction

One of the technologies that stand behind microservices popularity is Docker. The basic important terminology needed to get around in docker world is:

1. [image](https://docs.docker.com/engine/reference/commandline/images/#parent-command) - json template file + bundled user space in an archive
2. [container](https://www.docker.com/what-container) - a OS process spawned slightly differently than normal process, belonging to certain [namespace](https://en.wikipedia.org/wiki/Linux_namespaces) and limited with [cgroups](https://en.wikipedia.org/wiki/Cgroups)
3. [registry](https://docs.docker.com/registry/) - server with defined API containing your 'image database'
4. [Dockerfile]() - recepie how docker should build an image from source files

If you don't already have an account in dockerhub, largest public docker registry, go ahead and [create one](https://hub.docker.com/login/).

Then setup your environment like following but with your credentials:
```
source setup.sh
export DOCKER_PROFILE=[your_docker_profile_name]
docker login
```{{execute}} 

Now lets take a look at our first sample app in `~/app1`. Browse the code in the `main.go` file and familiarize yourself with it. Build the source into executable. Ask questions if you need any clarification

```
cd app1
go build main.go
```{{execute}}

### Build and share 
Second file to inspect is `Dockerfile`. The command [docker build](https://docs.docker.com/engine/reference/commandline/build/) is used to build the images locally. You can use [docker images](https://docs.docker.com/engine/reference/commandline/images/) to list all images available locally on your machine to verify your new image is among them. Then push it into your profile on dockerhub.

```
docker build . -t docker.io/$DOCKER_PROFILE/app1
docker images | grep 'app1'
docker push docker.io/$DOCKER_PROFILE/app1
```{{execute}}

Go to your dockerhub profile and see if the image is there: https://hub.docker.com/r/$DOCKER_PROFILE

##### Question 1.
You can see that sometimes the image name contains ':' such as in `centos:centos7`, also sometimes the images name is long and looks like URL, sometimes it is very short. Can you find out why the format differs and what the various formats mean?

### Run and see

The command [docker run](https://docs.docker.com/engine/reference/run/) is used to launch docker images. We also want to expose a port with `-p` and run the container in background daemonized with `-d`. You can re-map ports from within the container to be a different port available on the host network interface but you don't have to. Listing currently running containers is also handy when inspecting your system as well as killing them when you no longer want to run them.

```
docker run --name app1 -p 8080:8080 -d docker.io/$DOCKER_PROFILE/app1 
curl localhost:8080
docker ps | grep app1
docker kill app1
```{{execute}}

Now if you try to spawn a container with the same name, it will fail. Killed container does not equal to removed container and you may want to remove it entirely.
```
docker ps -a | grep app1
docker rm app1
```{{execute}}

##### Task 1.

Now you should be familiar with basic concepts. Try to edit the `main.go` to return different greeting and push into your registry under different tag. Exchange the image with your classmate sitting next to you and see if you can run his image. You will need the commands from the examples above and one more docker command not mentioned there, can you find which one it is?
