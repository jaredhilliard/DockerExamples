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
