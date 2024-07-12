# Docker Interview questions 


## Architecture  


<p align="center">
  <img src="https://github.com/user-attachments/assets/5340b7a3-a787-4f34-af8e-5c52e54cf4ed" width="600" title="Architecture" alt="Architecture">
  </p>
  


__1) What is Docker, and how does it differ from traditional virtualization?__
```yaml  
Docker is a tool  that allows developers to create, deploy, and run applications in the form of containers.

difference ===> 
- docker can not required multiple dependencies or libraries to run but for running perating systems we required multiple dependencies and libraries.  
- operating systems required seperated kernal for running, but in docker case it runs of host kernel means for running docker images we cannot required seperat kernel.
- only runtime libraries are installed thats why it cannot consume extra storage.
```  



__2) Explain the key components of Docker's architecture?__

```yaml
- Docker client :- With the help of the docker client, the docker users can interact with the docker. The docker command uses the Docker API.
- Docker engine/daemon :- Its Responsible for creating images and managing the containers. 
- Docker images :- Are the templates for the containers.  it contains all required packages or the libraries which is required for running the application.
- Docker containers :- When we run the images it beacmes the container. its like a process of linux os.
- Docker Registry :- These are are the storage images which are available publically..

```  


__3)  What are Docker containers, and how do they work?__  
```yaml 
docker containers are lightweight unit which contains all required packages which are needed for running the application.
because of containers we are not depend on single server. we deploy our application in the form of microservices.

```  
How They work --> 

<p align="center">
  <img src="https://github.com/user-attachments/assets/066490b4-3a76-415d-8dc8-37e47320e531" width="600" title="Architecture" alt="Architecture">
  </p>
  


__4) How do you create a Docker image? Can you explain the Dockerfile and its significance?__  


```yaml
we can create docker images with the help of Dockerfiles and its instuctions.

some key instructions in dockerfile are:-

FROM :- we specifies the base images from this. every image building process start from this instruction.
### FROM  nginx:latest   <name and tag>  

RUN :- For executing the command in the images
### RUN apt update -y 

COPY :- suppose if we want to copy the files from host machine in this case we use this instruction
### COPY .  .


```  
