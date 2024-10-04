#### docker images 
* image may contains both plan OS and application(IIS,Nginx/Apache,Tomcat,Websphere,Mysql-Server)
        
* image may only contains plan OS without application, when we create and start the containers from these images containers will be exited immediately , they wont be in running state. 

#### docker containers
* container is created using image

        docker create --nameubuntu01 ubuntu
        docker start  ubuntu01 
* To ensure the container should run in foreground and in iteractive mode.lets use different command

        docker run -dit --name ubuntu03 ubuntu

* This command pulls the image from docker hub and create and start the container in local system in iteractive mode.

* docker images are built from minimal base image to keep the image size small. we can only execute specific commands in the container, if we want other commands like vim, nano,if config, we can to add those in docker file to create seperate image , from the image we can create container. so the new container have those commands. 
* docker logs contianer --> for trouble shooting

* when we logout/exit from container this command terminates the container.

      docker attach containerid/containerName

* Two ways to login to the container 
 - docker exec -it container_name/bin/bash --> it creates the copy of main processes(startup comamnd). when container exit, it will exit from copy of start command. container still in running state.
 - docker attach container_name --> always connect to container main start up command(main process)when exit command run containers itself dies.
- docker start $(docker ps -a -q )
- docker rm ($docker ps -a -q)
 ### Inspect the objects(image,container, volumes,networks)

- docker image inspect image_name 
- docker inspect container_name
- docker network inspect network_name 
- docker volume inspect volume_name 

#### Linux Namespaces
- Linux has 7 types,  to work linux operating system in faster way it uses mechanism called as namespaces
  - PID(process isolation) - multi users is created and use there environment isolation
  - Network interfaces - network isolation beween application in system
  - IPC(interprocess communication)- programs running in one user login can communicate with another user programms
  - cgroups - the amount of resource allocations(cpu,ram) for all application that are executing in the linux system

  #### without docker we can create container using namespaces in linux.

  #### Docker contianer background
  - Inbackgorund it creates pid namespace,network interface namespace,Ipc,cgroups.
       
        docker run -dit --name container_name image_name
       
   - container is a isolated process, it creates
   PID namespace inside it has light weight OS and application. For that application  need network so network namespace is created that applciation needed storage it creates storage namespace, To run the application it needs cpu and memory it cretaes cgroups.
      
         docker run -dit --name container_name image_name

  #### networking
  - docker network ls
       - bridge network 
       - host network
       - none
