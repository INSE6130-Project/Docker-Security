Docker Installation (Ubuntu):

	sudo apt-get remove docker docker-engine docker.io containerd runc
	sudo apt-get update
	sudo apt-get install ca-certificates curl gnupg lsb-release
	sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
	sudo echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
	$(lsb_release -cs) stable" | sudo tee /etc/apt/	sources.list.d/docker.list > /dev/null
	  
	sudo apt-get update
	sudo apt-get install docker-ce docker-ce-cli containerd.io

List available images:

	sudo docker images
	sudo docker image ls
	
List containers:

	sudo docker ps #(running)
	sudo docker ps -a #(all)

Setting up local Docker Registry:

	sudo docker pull registry
	
Add localhost link to insecure registry url in /etc/docker/daemon.json

	sudo echo '{"insecure-registries" : ["localhost:5000"]}' > /etc/docker/daemon.json

	sudo docker run -d -p 5000:5000 --restart=always --name registry registry:latest

Hosting a docker image:

	<Write Dockerfile> #file:///home/cyc0rpion/DockerSecurity/Resources/Dockerfile_Ubuntu_SensitiveInfo.txt

	sudo docker build -t ubuntu:new
	sudo docker tag ubuntu:new localhost:5000/ubuntu:new
	sudo docker push localhost:5000/ubuntu:new
	
Delete running containers of ubuntu:new

	sudo docker rm <containerId>

Delete local copies of ubuntu:new :

	sudo docker image rm ubuntu:new
	sudo docker image rm localhost:5000/ubuntu:new

Pull new image from docker registry

	sudo docker pull localhost:5000/ubuntu:new

Running docker container from ubuntu:new

	sudo docker run localhost:5000/ubuntu:new
	
	
Running docker container with ssh port accessible

	
	sudo docker run -it -d -p 22:22 ubuntu:new


Running docker container with ssh port accessible and mounted docker socket

	
	sudo docker run -it -d -p 22:22 -v /var/run/docker.sock:/var/run/docker.sock ubuntu:now3
	
	
Running docker container with sys-admin capabilities but disabled privy flag


	sudo docker run --rm -it -d --cap-add=SYS_ADMIN --security-opt apparmor=unconfined ubuntu:now2 bash
	
To import docker in python3
1. sudo apt install python3-pip
--- will get an error : so use this command -> sudo apt install python3-pip --fix-missing.
2. pip install docker.
	
