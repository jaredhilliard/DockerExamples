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
> docker rm containerId

We need not type out the entire container ID, it is in fact quite a bit longer than what we are shown.  If the container ID you are shown is effa1cc3c9f1, you only have to type enough to uniquely identify the container you want to remove.  If there are no other container IDs beginning with e, the following is sufficient:
> docker rm e

If we have a lot of stopped containers, and no reason to keep records of them around, we can simply use
> docker container prune -f

The f flag will force the removal of every stopped container without asking for permission.

Alright, let's run a few more containers available on the *Docker Hub* that we've seen before.
> docker run -d -p 8085:80 nginx

The d flag causes the container to run in the background.  The p flag tells the linux vm to open port 8085, and route any traffic to port 80 in the nginx container.

> docker run -p 8088:8080 jenkins

Navigate to your Amazon Linux server on port 8088 (this is your Public DNS on the VM Description page).  Are you able to proceed with installing Jenkins?  If not, what might you need to fix?

Make sure to modify the security group so that port 8088 is open to the world (port 8080 will be open on the container by default).

Now, what good does running jenkins inside a container do for us?  This isn't a teachable moment, I'm generally curious and a little bit flabbergasted.  What would we do with this?

Oh well, it's a cool thing you can do, let's move on.

Let's discuss storage.  When a container writes files, it writes them *inside* of the container.  If we stop the container, if the host machine restarts, if the container is moved to a different node, if a solar flare causes some key electrons to change their state and overwrite some bits, all of the data is lost.  If you run multiple copies of the same container, they all have their own data.

What we want is for containers to be stateless, all data stored in an external database such as a SQL server. But if we want to store files in persistent storage, we use volumes.  In a production scenario, this might be something like Amazon S3 on AWS.  But we don't have that kind of cash, or that kind of need, so let's look at using local storage on our VMs.
> docker run -v /your/dir/:/data/db -d mongo

This will ensure any data written into the /data/db container inside the directory is *actually* written to the /your/dir/ directory on the host system.  Thus we can have multiple MongoDB containers running on our host system all referring to the same persistent storage and users will never know the difference, solar flares be damned.

Now, what if we want to build our own images?

