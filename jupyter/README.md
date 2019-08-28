# Docker test

To launch a Docker container with the image defined in `Dockerfile`, first you need to build the image (possibly, it's been already built and it's updated, but rebuild it for good measure). To rebuild the Docker image,
1. Open Docker.
2. open a shell, navigate to the directory where this readme is and run
```
docker build --tag=docker-test .
```

To launch the container and automatically have it run a Jupyter server, run
```
docker run -p 8888:8888 docker-test
```
If you open `localhost:8888` in a browser you should see the Jupyter server page.

To launch the container and have access to its shell, on the other hand, run
```
docker run -it -p 8888:8888 docker-test bash
```
From here you'll be able to see whatever is inside the container (not much) and launch Jupyter manually with
```
jupyter notebook --ip=0.0.0.0 --port=8888 --allow-root --NotebookApp.token=''
```

### File persistence

The content of this same directory is copied by design into the container "virtual filesystem", but the opposite is not true: whatever file you create inside the container (e.g. Jupyter notebook) will note be available from outside the container and will be lost forever when the container is shut down. If you access the container's shell, though you will have access to its filesystem and files will be visible as long as the container exists.

If we want the container to be able to access some part of the filesystem of the host, one option is to mount it when we launch the container itself specifying the `-v` option of `docker run`. If e.g. we want to be able to write to the `./data/` directory, we can run
```
docker run -it -p 8888:8888 -v /<ABSOLUTE_PATH>/data:/app/data docker-test bash
```
where the syntax is `-v <path to host dir>:<path to container dir>`. Note that we can only use absolute path when doing this.

## Sources

* [Docker RUN vs CMD vs ENTRYPOINT](http://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/)
