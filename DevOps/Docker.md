# Docker Interview questions 


## Architecture  


<p align="center">
  <img src="https://github.com/user-attachments/assets/5340b7a3-a787-4f34-af8e-5c52e54cf4ed" width="600" title="Architecture" alt="Architecture">
  </p>
  


__1) What is Docker, and how does it differ from traditional virtualization?__
```yaml  
Docker is a platform that allows developers to create, deploy, and run applications in containers.

difference ===> 
- Operating systems required multiple dependencies and libraries to run, but in docker case we can not required multiple dependencies as reason this are lightweight.
- operating systems required seperated kernal for running, but in docker case it runs of host kernel means for running docker images we cannot required seperat kernel.
- only runtime libraries are installed thats why it cannot consume extra storage.

```  


