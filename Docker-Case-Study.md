# Docker Case Study
## Problem : Automate infra allocation for L&D
### Requirements : 
* Dynamic allocation of Linux systems for users
* Each user should have independent Linux System
* Specific training environment should be created in Container
* User should not allow to access other containers/images
* User should not allow to access docker command
* Monitor participants containers
* Debug/live demo for the participants if they have any doubts/bug in running applications
* Automate container creation and deletion
### Allocate Linux Containers for users :
 1. Dynamic allocation of Linux systems for users can be achieved by the shell script `user_containers.sh`.Such a script
    would create docker for each container.
 * `users.txt`
   ```
    user1
    user2
    user3
    user4
    user5
    ```
  * `user_containers.sh`
  ```
  echo -n "enter user file name: "
read file

while read user
    do
        docker create -it --name $user <Img> /bin/bash
    done < $file
  ```
  Execution of the above script would create a docker container for each user.
 2. User can use the container allocated to him using the shell script `use_container.sh`.
 * `use_container.sh`
 ```
 #! /bin/bash
echo -n "Enter usename: "
read name
docker start $name
docker attach $name
 ```
This allows the user to enter his/her linux system. User has access to only his system.
### Monitoring the Container : 
Monitoring the activities of a particular user can be achivied by running the script `monitor_container.sh`.
* `monitor_container.sh`
```
#! /bin/bash

echo -n "Enter the container name to be monitored : "
read name
docker logs -f $name
```
### Deletion of Containers : 
Containers can be deleted using the script `delete_container.sh`.
*`delete_container.sh`
```
echo -n "Enter the user list file : "
read file

while read user
  do
    docker stop $user
    docker rm $user
  done > $file
```
Above shell scripts can be executed by using the command : 
```
sh <shell script>
```













