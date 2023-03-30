## Writing your first Dockerfile

To build a Docker image, you need to create a Dockerfile. It is a plain text file with instructions and arguments. Here is the description of the instructions we're going to use in our next example:

* **FROM** -- set base image
* **COPY** -- execute command in container
* **CMD** -- set executable for container

You can check [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more details.

Let's create an image that will recreate yesterday's nginx website with your custom made `50x.html` page, but this time, we bundle the `50x.html` page INSIDE of the Docker image instead of mounting a local directory.

Place a file name **Dockerfile** in **examples/nginx** directory with the following contents:

```dockerfile
FROM nginx:latest

COPY 50x.html /usr/share/nginx/html

CMD ["nginx", "-g", "daemon off;"]
```
*Note: The CMD that I used is the same one that the original `nginx` images uses, so our new image should behave the same as the original `nginx` image.*

Then, also add yesterday's `50x.html` file to the same directory. It's now time to build the image.

Go to **examples/curl** directory and execute the following command to build the image:

```bash
docker build . -t test-nginx
```

* **docker build** command builds a new image locally.
* **-t** flag sets the name tag to an image.

Now we have the new image, and we can see it in the list of existing images:

```bash
docker images
```

Run the nginx container and bind the container port 80 to your machine's port 80.

Go to http://localhost/50x.html. If your page loads succesfully, it means you can now distribute this Docker image (and website) to any server in the world!

**SHOW THE RESULT TO YOUR TEACHER**

## Writing another Dockerfile

In this second Docker image, we will use the following commands.

* **FROM** -- set base image
* **RUN** -- execute command in container
* **ENV** -- set environment variable
* **WORKDIR** -- set working directory
* **VOLUME** -- create mount-point for a volume
* **CMD** -- set executable for container

Let's create an image that will get the contents of the website with **curl** and store it to the text file. We need to pass website url via environment variable **SITE_URL**. Resulting file will be placed in a directory mounted as a volume.

Place a file name **Dockerfile** in **examples/curl** directory with the following contents:

```dockerfile
FROM ubuntu:latest
RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y curl \
    && rm -rf /var/lib/apt/lists/*
ENV SITE_URL http://example.com/
WORKDIR /data
VOLUME /data
CMD sh -c "curl -Lk $SITE_URL > /data/results"
```
In this Dockerfile, we actually install some software (`curl`) into our image. It is a very common usecase that if you distribute your software/website inside a Docker image, that you also install the software that is required by it.

Now, build the image.

After building the image, run it, but add the following parameter to mount the `/data/` folder in the container to the `vol` directory in your current directory: `-v "%cd%"/vol:/data/:rw` (if you are on Ubuntu, replace `%cd%` with `$(pwd)`)

Now, look at the results in the `vol` folder.

Let's try to override the default `ENV SITE_URL http://example.com/` at runtime with **facebook.com** by running the last command again, but adding `-e SITE_URL=https://facebook.com/`

Now, look again at the results in the `vol` folder.

**SHOW THE RESULT TO YOUR TEACHER**

*adapted from: https://github.com/alexryabtsev/docker-workshop*