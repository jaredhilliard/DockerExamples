# DockerExamples
A repository of simple docker images for teaching purposes.  Installation instructions are for Amazon Linux EC2, and are stolen directly from https://gist.github.com/npearce/6f3c7826c7499587f00957fee62f8ee9.  Note that as of this commit, yum works just fine, no need to involve the amazon-linux-extras package manager.

First we need install docker.  Run the following commands:
1. sudo yum update
2. sudo yum install docker
3. sudo service docker start
4. sudo usermod -a -G docker ec2-user
5. sudo chkconfig docker on
6. sudo reboot

1. This is just generally a safe practice before any installation.
2. Obvious.
3. Start the docker service.
4. Add ec2-user to the docker group to avoid any permission issues.
5. Makes docker service start on start up.
6. Reboot to verify it all runs fine on it's own. 

You will also need git to use the docker auto-building feature.  So if it isn't already installed:
1. sudo yum install git
2. git config --global user.name "username"
3. git config --global user.email "email@website"
