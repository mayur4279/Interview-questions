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
=================================
Docker files 
=================================

-----------------------------
1) FROM  
-----------------------------
Syntax:- FROM  <image>[:<tag>] [AS <name>]
Example:- FROM  nginx:latest  AS my_nginx  

why we use??   
This Instruction is used for pulling the base image from  docker hub 
its the first instruction  for building the application  

-----------------------------
2) RUN
-----------------------------
Syntax:- RUN <command>  
Example:- RUN echo "this is my website" >>  /usr/share/nginx/html/index.html 
          RUN apt-get update && apt-get install -y apache2

why we use??  
-The RUN instruction in a Dockerfile is used to execute commands during the image build process. These commands can be used for various purposes...
*Copying files
*Running scripts
*Performing configuration tasks
- This Command can increase the size of image so use them efficiently.  
- We can run multiple RUN instructions to execute sequence of commands.  
- Or we can use below option as well for running multiple commands using RUN instruction 

RUN apt get -y update  

-----------------------------
3) EXPOSE 
-----------------------------
Syntax:- EXPOSE <port> [<port>/<protocol>...]
Example:- Expose 80/tcp   --> if you don't specify a protocol the default is tcp 
          Expose 80/udp   

why we use??   
- Describe which ports your application is listening on.
- For example we are building nginx server image, in that case we required port 80 to be open 

-----------------------------
4) COPY 
-----------------------------
Syntax:- COPY <source_address> ... <destination_address>
Example:- COPY  index.html  /var/www/html/   

Copies files or directories from the host machine (your development environment) into the container's file system.
Useful for including application code, configuration files, or other resources.
Supports wildcards (*) for copying multiple files or directories that match a pattern.

---------------------------------------------
5. ADD (Similar to COPY but More Versatile):
---------------------------------------------
Syntax: ADD <source>... <destination>
Example: ADD requirements.txt /app (Adds a file and unpacks it if it's a compressed archive)
         ADD https://example.com/file.tar.gz /app
		 
Purpose:
Similar to COPY, but can additionally:
Unpack compressed archives (e.g., .tar.gz, .zip)
Interpret remote URLs as sources (e.g., ADD https://example.com/file.tar.gz /app)

-------------------------------------------
5. WORKDIR (Set Working Directory):
-------------------------------------------
Syntax: WORKDIR <path>
Example: WORKDIR /app
Purpose:
Sets the working directory for subsequent instructions in the Dockerfile.
Useful for organizing commands and making them more readable.
Doesn't create a new layer unlike RUN.

-------------------------------
6. CMD (Default Command):
-------------------------------

Syntax: CMD ["<command>", "<argument>", ...] (Optional, multiple CMD instructions are allowed)
Example: CMD ["nginx", "-g", "daemon off;"]
Purpose:
Specifies the default command to be executed when the container starts.
Only the last CMD instruction in the Dockerfile is considered.
Use ENTRYPOINT for more control over container execution.

---------------------------------------
7. ENTRYPOINT (Executable Behavior):
---------------------------------------

Syntax: ENTRYPOINT ["<command>", "<argument>", ...]
Example: ENTRYPOINT ["python", "/app/main.py"]
Purpose:
Similar to CMD, but provides more control over the container's execution.
The specified command becomes the container's process 1.
Arguments passed to docker run are appended to the ENTRYPOINT command.
Prefer ENTRYPOINT for defining the executable behavior of the container.

------------------------------------
8. ENV (Set Environment Variables):
------------------------------------

Syntax: ENV <variable_name> <variable_value>
Example: ENV PORT 8080

Purpose:
Sets environment variables within the container image.
These variables can be accessed by processes running inside the container.
Useful for configuration values, database connections, or API keys.

-----------------------------
9. USER (Set User):
-----------------------------

Syntax: USER <username>[:<group>]
Example: USER nobody:nogroup

Purpose:
Specifies the user under which processes will run inside the container.
Defaults to the user who built the image (usually root).
Use with caution to minimize security risks, especially in production environments.  

----------------------------------------------
10. HEALTHCHECK (Liveness/Readiness Probes):
-----------------------------------------------
#code 
HEALTHCHECK [OPTIONS] CMD <command> [ARGUMENTS...]
HEALTHCHECK [OPTIONS] INTERVAL=<interval> RETries=<retries> <command> [ARGUMENTS...]

Example: HEALTHCHECK --interval=10s --retries=5 CMD ["curl", "-f", "http://localhost:8080/health"]

Purpose:
Defines health checks for your container.
Can be used to determine if the container is alive (liveness) or ready to receive traffic (readiness).
The specified command is executed periodically to assess the container's health.

----------------------------
11) LABEL (Metadata):
---------------------------- 

Syntax: LABEL <label_name> <label_value>
Example: LABEL maintainer="John Doe <john.doe@example.com>"

Purpose:
Adds metadata to the image for informational purposes.
Labels can be used to describe the image, track ownership, or define deployment configurations.
Often used by container management tools for organization and automation.

--------------------------------------
12) SHELL (Set Shell Environment):
--------------------------------------
Syntax: SHELL ["<shell>", "<arguments>"] (Optional)
Example: SHELL ["/bin/bash", "-c"]

Purpose:
Sets the default shell environment for the container.
Defaults to /bin/sh.
Useful for specifying a different shell interpreter (e.g., /bin/bash) or customizing its arguments.

--------------------------------
13) VOLUME (Persistent Data):
--------------------------------

Syntax: VOLUME ["<path1>", "<path2>", ...]
Example: VOLUME ["/data"]

Purpose:
Defines directories or named volumes that persist data outside the container's file system.
Useful for storing data that needs to be preserved between container restarts or across multiple containers.
Docker doesn't create or manage volumes automatically. You need to create them using docker volume create before running the container.

--------------------------------------------------
14) ONBUILD (Instructions for Subsequent Builds):
--------------------------------------------------

Syntax: ONBUILD <INSTRUCTION>
Example: ONBUILD COPY . /app

Purpose:
Specifies instructions that are executed only when the current image is used as a base image for another build.
Useful for setting up defaults or environment variables for child images.
Instructions within ONBUILD stages don't contribute to the final image of the current build.

----------------------------------
15) ARG (Build-Time Variables):
----------------------------------
Syntax: ARG <variable_name>
Example: ARG APP_NAME
Purpose:
Defines build-time variables that can be passed when building the image.
Used in subsequent instructions (e.g., FROM) to dynamically reference values.
Provides flexibility in customizing the image build process without modifying the Dockerfile itself.

-----------------------------------
16) MAINTAINER (Image Maintainer):
-----------------------------------
Syntax: MAINTAINER "<name> <email>" (Optional)
Example: MAINTAINER "John Doe <john.doe@example.com>"

Purpose:
Adds metadata to the image, indicating who maintains it.
Useful for tracking ownership and responsibility for the image.

---------------------------------------
17) STOPSIGNAL (Specify Exit Signal):
--------------------------------------- 
Syntax: STOPSIGNAL <signal> (Optional)
Example: STOPSIGNAL SIGQUIT

Purpose: Specifies the system call signal that will cause the container to exit. Defaults to SIGTERM. 
Useful for customizing how the container shuts down.


```  
