
# Welcome

![Bayport](/Bayport_Logo.png)

Welcome to Bayport's DevOps skills assessment.
Please fork this repository and answer any questions on this markdown document.

# Linux
* What is the command to list the contents of a direcory, line by line and ordered by size ascending in human readable format? 
	ls -laShr
* How would you add a DNS server to a network interface in Linux? 
	vi /etc/sysconf ig/network-scripts/interfacename
* If the DNS server you've just added is not reachable, how can you get any particular hostname to resolve locally? 
	add it in /etc/hosts
* How would you check for SELinux related errors? 
	/var/log/messages
* Write the commands to add 30GB disk space to a logical volume named "docker" that belongs to a logical group named "docker-group". 
	lvextend -L +30Gb /dev/docker-group/docker
* In the root of this repository, create a Bash script called "listit.sh", when executed, this script must do the following (in order):
    * Create a file called directories.list that contains the directory names only of the current directory.
    * Add a line at the beginning of the directories.list file that reads "line one's line".
    * Output the first three lines of directories.list on the console.
    * Accept an integer parameter when executed and repeat the previous question's output x amount of times based on the parameter provided at execution.
	
	#!/bin/bash
	ls >> listit.sh
	sed -i -e '1iline one's line\' directories.list
	head -3 directories.list
	
	COUNTER=0
    
    echo "guess a number "
    read NUMBER
    
    while [ $NUMBER != $COUNTER ]
    do
      echo "you guessed wrong"
      read NUMBER
      if [ $NUMBER = $COUNTER ]
      then
      echo "YOU GUESSED RIGHT!!!!!!!"
      fi
    done

	
	
* Commit and push your changes.

# Docker
* In the root of this repository, create a Dockerfile that is based on the latest mariadb image.
* Expose port 3307.
    * Define an evironment variable called BRUCE with a value of WAYNE.
    * Run a command that will output the value from BRUCE into a file called BATCAVE in the root directory of the container. 
touch /root/Dockerfile

within Dockerfile:

FROM alpine:3.8
RUN apk update
RUN apk add –no-cache mariadb
EXPOSE 3307/tcp
ENV BRUCE WAYNE
ENTRYPOINT  echo "$BRUCE" > /root/BATCAVE

* Create a Bash script in the root of this repository called FLY.sh that will do the following:
    * Install Docker if it is not yet installed.
    * Ensure the installed version of Docker is the latest version available.
    * Start a container using the image you've craeted above with your Dockerfile - this container must run as follows:
        * It must be named ALFRED.
        * It must mount /var/lib/mysql to the host operating system to /var/lib/mysql.
        * It must mount /BATCAVE to the host operating system.
    * Checks whether a container exists called ALFRED and if it does, removes an recreates it.
    * Create a schema in the database called "wayneindustries" with one table in it called "fox" with columns "ID" and "Name".
    * Insert an entry with ID "50" and Name "BATMOBILE".
* Create an encrypted file called "secret" in the root of this repository that contains the root password of the database (the password must be "thisisadatabasepassword123456789!").
* Change your Bash script to start the conainer using the root password from the "secret" file.
* Commit and push your changes.

#!/bin/bash
curl -fsSL get.docker.com -o get-docker.sh
sh get-docker.sh
docker build -t ALFRED /root/
docker stop ALFRED || true && docker rm ALFRED || true
docker run \
--detach \
--name=ALFRED \
--env="MYSQL_ROOT_PASSWORD=thisisadatabasepassword123456789!" \
--publish 6603:3306 \
--volume=/root/BATCAVE \
--volume=/storage/docker/mysql-data:/var/lib/mysql \
mysql
docker exec -it mysql1 mysql -uroot -p
CREATE DATABASE wayneindustries
use wayneindustries
CREATE TABLE fox 
ALTER TABLE fox
ADD COLUMN ID
ADD COLUMN Name
INSERT INTO table_name (ID, Name)
VALUES (50, BATMOBILE);


# General
* How would you ensure any change made to this Dockerfile is source controlled, approved, tested and deployed. Explain which tools you will use as if this was going into a production environment. 
git and local github repo where you can run pull request and approve merge requests for any changes. You can therefore have certain maintain approvals of any changes
* Commit and push your changes.