# Useful Commands

Let's run our first docker container.
> docker run hello-world
So, what just happened?

1. You commanded docker to create and run a container based on the hello-world image.
2. Docker tried to find the image on the machine.  Since it isn't there, Docker downloads the image from the default registry, the *Docker Hub*.
3. Docker created a container based on the hello-world image.
4. The hello-world image does as one would expect, outputs text to the console.
5. Since there is nothing else for it to do, the container stops. 

If you run the same command again, the image is already on the disk, so docker just outputs the text.

Let's look at our docker processes using
> docker ps 
docker ps works as you would expect, it shows active docker processes.  We can see a list of stopped processes using 
> docker ps -a
Try running hello-world a few more times.

As you can imagine, a production system might have docker containers running and stopping constantly.  The list of stopped processes can get rather crowded.  Let's remove some of them.
> docker rm <CONTAINER ID>
We need not type out the entire container ID, it is in fact quite a bit longer than what we are shown.  If the container ID you are shown is effa1cc3c9f1, but there are no other container IDs beginning with e, you only have to type enough to uniquely identify the container you want to remove.
> docker rm e
If we have a lot of stopped containers, and no reason to keep records of them around, we can simply use
> docker container prune -f
The f flag will force the removal of every stopped container without asking for permission.
