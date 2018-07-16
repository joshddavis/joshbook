# Basic Commands

**docker run ubuntu** - will will pull down the image from docker hub if you don't already have it. it only needs to do this the first time

**docker ps** - lists all running containers and some basic info regarding them (container id, image, status)

**docker ps -a** - lists all running and previously executed containers

**docker stop [name]** - stops the container based on the name...can also use id

**docker rm [name]** - deletes a stopped container for good

**docker images** - lists downloaded images

**docker rmi [image]** - used to remove images for good...must ensure no containers are currently using....

**docker pull ubuntu** - only downloads the image

*docker containers are meant to run applications...if there's nothing running, it stops the container immediately*

**docker run -d Ubuntu sleep 1000** - keeps the container alive (sleeping) for a thousand seconds before stopping it....the -d flag runs the command in the background so you can stay at your prompt

**docker exec [name] cat /etc/hosts** - executes a command on a running container...in this example it runs the cat command which returns the contents of the listed directory
