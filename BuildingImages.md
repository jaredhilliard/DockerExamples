# Building Images

Before we get into building images, we need to discuss the magical fairy land from which they came, the *Docker Hub*.  Go ahead and create a Docker Hub account if you don't already have one, as we are going to build some images and push them to our Ducker Hubs.

Every image you attempt to run that isn't available locally is downloaded from a registry. Images published to a registry must be named like
> \<repository\_name\>/\<name\>:\<tag\>

Every image is created using the *docker build* command and a *Dockerfile* file.  The Dockerfile need not be named Dockerfile, but it usually is.  The docker build command will look for a file named Dockerfile unless told otherwise. If you keep your docker projects in separate directories, with their own github repositories, it is traditionally just called 'Dockerfile'.

The Dockerfile describes how the image should be built, and always starts witha FROM command, every image is based on another base image.

Cd to the FatHelloWorld directory, so that we may take a look at the FatHelloWorld Dockerfile.  We build on top of the debian image, version 8.  Once the debian container is running, it will issue the command "echo Hello world" and stop.

If we're happy with our instructions, we can build our image using 
> docker build -t hello .

The -t flag is used to name the resulting image 'hello'  We can build an image without a tag, it will have an auto-generated unique ID.  Note the dot.  We are specifying that the Dockerfile is in the current directory, and just named Dockerfile.  If we were cheeky, and put our Dockerfile somewhere else with a funky name, we could use the -f flag.

Our resulting image is named hello, and stored locally. We can now run it like any other image:
> docker run --rm hello

The --rm option automatically removes the container from the process list after it is stopped.

Now, what if we want to publish our images? 

Publishing is a 3 step process.
1. docker build
2. docker login
3. docker push

Go ahead and run
> docker login

Anything we attempt to push needs to at least be tagged with the repository name and the image name, i.e.
> docker push \<repository\_name\>/\<image\_name\>

or

> docker push \<repository\_name\>/\<image\_name\>:\<tag\_name\>

If you don't specify a tag, Docker will just use 'latest'.  Traditional tags are things like version numbers or git commit hashes.

If we want to rename a docker image in order to publish it, we can use:
> docker tag \<current\_name\> \<repository\_name\>/\<current\_name\>

Let's demonstrate how easy it easy to tie docker builds to git pushes.

