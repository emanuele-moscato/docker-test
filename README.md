# Using Docker

Here are some basic facts on how to use Docker. A prerequisite for all this is to install Docker Desktop Community ("CE") and to have it running before hitting any of the commands below.

## Pulling an image from Docker Hub

To pull an image given an image name (and a specific tag, if required), run
```
docker pull <IMAGE_NAME>[:<TAG>]
```
This will pull the built image from Docker Hub to the local Docker repository, where it will be ready to be run.

## Running a built image

To run an image, run
```
docker run <IMAGE_NAME>[:<TAG>]
```

## Building an image

To build an image from a Dockerfile, navigate to where the file is an run
```
docker build --tag=<IMAGE_NAME> .
```
where the image name is what we'll use to run it.

## Example: an image with Python 3.8

Let's say we want to run the image for Python 3.8, which is in Docker Hub. Its hose name is `python` and its tag is (as of now) `3.8.0a4`. We need to run
```
docker pull python:3.8.0a4
```
If we run the image with
```
docker run python:3.8.0a4
```
the container will be created and immediately exit, as no command is specified for the image. If we want to access the container's command line, we can run
```
docker run -it python:3.8.0a4 bash
```

## Installing Linux packages in a container

If we are running a container that inherits e.g. from the Ubuntu base image and we are accessing its command line, we won't immediately be able to install Linux packages by running `sudo apt-get install <PACKAGE_NAME>`.

To do this, first remember __not to use `sudo` in a container's command line__, then just update `apt-get` by running
```
sudo apt-get update
```
Now we'll be able to install Linux packages by running
```
apt-get install <PACKAGE_NAME>
```

## Other commands

The Docker images the local client is aware of are available by running `docker images -a`. Without the `-a` tag, we are only shown the most recent images.

Sometime the `REPOSITORY` and `TAG` fields for an image contain `<none>`. This is the case e.g. for intermediate images (which a child image inherits from) and is normal. For more information on this: https://medium.com/@joeydlee95/docker-images-none-b0141aa740c5
