# Introduction to Containers and Docker

https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/container-docker-introduction/

# What is Docker?

https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/container-docker-introduction/docker-defined

### Terminology

https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/container-docker-introduction/docker-terminology

### Docker containers, images, and registries

https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/container-docker-introduction/docker-containers-images-registries


# Labs

## Local exercises

### Using Portainer to manage Docker

https://portainer.io/overview.html


### **Dotnet console Applications** 

https://docs.microsoft.com/en-us/dotnet/core/docker/docker-basics-dotnet-core

#### Introduction to the Dotnet console samples

https://github.com/dotnet/dotnet-docker/tree/master/samples/dotnetapp

#### Development process for Dotnet Console Docker Applications

https://github.com/dotnet/dotnet-docker/blob/master/samples/dotnetapp/dotnet-docker-dev-in-container.md



### **ASP.net Core Applications** 

https://docs.microsoft.com/en-us/dotnet/core/docker/building-net-docker-images

#### Introduction to the ASP.net Core samples

https://github.com/dotnet/dotnet-docker/tree/master/samples/aspnetapp

#### Development process for ASP.net Core Docker Applications

https://github.com/dotnet/dotnet-docker/blob/master/samples/aspnetapp/aspnet-docker-dev-in-container.md



## Online sandbox exercises

https://www.katacoda.com/courses/docker



# Appendix - A - Commands

Note <container> is either a container id, or a container name (if such is given to a container with the --name option on start). Both can be obtained with the "docker ps -a" command. <image> is either an image id, or an image name. Both can be obtained with the "docker image" command. Do not confuse with container id/name!

    docker ps                           # List running instances
    docker ps -a                        # List all instances
    docker inspect <container>          # Instance details
    docker top     <container>          # Instance processes
    docker logs    <container>          # Instance console log
    docker port    <container>          # Shows container's port mapping. The same can be seen with "docker ps" though (row - "PORTS")
    docker diff    <container>          # Shows changes on container's filesystem. Will produce a list of files and folders prefixed by a
                                        # character. "A" is for "added", "C" is for changed.
    docker stats   <container>          # Shows the consumed by the container resources (memory, CPU, network bandwidth)


​    
​                                          

    docker run -i -t ubuntu /bin/bash   # New instance from image. "-i" is for "interactive" and "t" is for terminal. Without "it" it
                                        # won't be interactive - you will get a shell/terminal, but will not be able to type anything onto 
                                        # it. Without "t" you will not get a terminal opened. The command will run and exit.
                                        
    docker run -i -t --rm ubuntu /bin/bash # If you need a one-time container, then use the --rm option. Thus, once you exit the container,
                                        # it will be removed                                  


    docker start   <container>
    docker restart <container>
    docker stop    <container>
    docker attach  <container>
    docker rm      <container>          # Removes / deletes a container (do not confuse with the "rmi" command - it removes an image!).
                                        # The container must be stopped in beforehand.
    
    docker cp '<id>':/data/file .       # Copy file out of container
    
    docker images                       # List locally stored images
    docker rmi <image>                  # Removes / deletes a locally stored image
    docker save -o <tarball> <image>    # Saves a local image as a tarball, so you can archive/transfer or inspect its content
                                        # Example: docker save -o /tmp/myimage.tar busybox
    docker load < <tarball>		    	# Loads a local image from a tarball						
    docker history <image>              # Shows image creation history. Useful if you want to "recreate" the Dockerfile of an image -
                                        # in cases where you are interested how the image has been created.

## Dockerfile Examples

Installing packages

    FROM debian:wheezy
    RUN apt-get update
    RUN apt-get -y install python git

Adding users

    RUN useradd jsmith -u 1001 -s /bin/bash

Defining work directories and environment

    WORKDIR /home/jsmith/
    ENV HOME /home/jsmith

Mounts

    VOLUME ["/home"]

Opening ports

    EXPOSE 22
    EXPOSE 80

Start command

    USER jsmith
    WORKDIR /home/jsmith/
    ENTRYPOINT bin/my-start-script.sh


​	
### Appendix B - Importing a docker image if you have bandwidth issues

(To export: docker save microsoft/aspnetcore:2.1 -o microsoft_aspnetcore_2.1.tar)


docker load < microsoft_aspnetcore-build_2.1.tar
docker load < microsoft_aspnetcore-build_latest.tar
docker load < microsoft_aspnetcore_2.1.tar