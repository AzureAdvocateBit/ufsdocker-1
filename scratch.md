#Docker-basics

https://docs.microsoft.com/en-us/dotnet/core/docker/docker-basics-dotnet-core

##open bash
```bash
cd /c/projects/docker

dotnet new console
dotnet run

dotnet publish -c Release -o out

docker build -t dotnetapp-dev .
docker run --rm dotnetapp-dev Hello from Docker
```




#Samples

#.NET Core Docker Sample
-->open bash

```bash
cd /c/projects/docker/dotnet-docker/samples/dotnetapp/dotnetapp
dotnet run

cd /c/projects/docker/dotnet-docker/samples/dotnetapp/

docker build -t dotnetapp .
docker run --rm dotnetapp Hello .NET Core from Docker
docker build --target testrunner -t dotnetapp:test .
winpty docker run --rm -it dotnetapp:test
```




#Develop .NET Core Applications in a Container

-->open command prompt

```bash
cd C:\projects\docker\dotnet-docker\samples\dotnetapp

docker run --rm -it -v C:\projects\docker\dotnet-docker\samples\dotnetapp:/app/ -w /app/tests microsoft/dotnet:2.1-sdk dotnet watch run

docker run --rm -it -v C:\projects\docker\dotnet-docker\samples\dotnetapp:/app/ -w /app/tests microsoft/dotnet:2.1-sdk dotnet watch test

docker run --rm -v C:\projects\docker\dotnet-docker\samples\dotnetapp:/app -w /app/dotnetapp microsoft/dotnet:2.1-sdk dotnet publish -c Release -o out
```




#ASP

##Run locally
```bash
cd C:\projects\docker\dotnet-docker\samples\aspnetapp\aspnetapp
dotnet run
```



##Build docker
```bash
cd C:\projects\docker\dotnet-docker\samples\aspnetapp
docker build -t aspnetapp .
docker run --name aspnetcore_sample --rm -it -p 8000:80 aspnetapp
```


-->http://localhost:8000

#Develop ASP.NET Core Applications in a Container

```bash
docker run --rm -it -p 8000:80 -v C:\projects\docker\dotnet-docker\samples\aspnetapp:/app/ -w /app/aspnetapp microsoft/dotnet:2.1-sdk dotnet watch run
```


-->http://localhost:8000