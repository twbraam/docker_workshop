# Docker exercise
The following exercise is done from either a Ubuntu or Windows Terminal

## Hello world
1. Run `docker images` there should be nothing there
2. Now run `docker run hello-world`. This is a very simple Docker image that can do print a message.
3. If this works, did you see how it says that it cannot find `hello-world` locally and it downloaded it automatically?
4. Now check your images again. Inspect all columns and their values carefully

## Run a simple Linux OS
1. Run `docker run ubuntu`. Look at how tiny this image is compared to a full Windows or Linux installation!
2. What happened... nothing, right? Normally when you create and distribute a Docker image, you also tell it which
   command it should run. In `hello-world` that was printing that message. In `ubuntu` the command that is run (`/bin/bash`), exits immediately so we see nothing.
3. Now run `docker ps` to show all current running images, how many are there? Once the last command from step 2 has exited, the docker container will also stop. You can see all stopped images using `docker ps -a`
4. Let's interrupt the exiting of the container by running `docker run -it ubuntu` (The `-i` parameter means "interactive"). Running with this command also attaches our current shell to the docker image.
5. Type `exit`. This causes the main command (remember, step 2?) of the image to exit. What happened to the container now?
6. As long as this last command does not exit, the container will stay alive. Rerun `docker run -it ubuntu` and try to get out of the container without exiting `/bin/bash`.
7. Once you have done that, query all running docker containers again to make sure that it is still there
8. Now run `docker attach <container id>` to attach to it again.
9. Play around within the container to convince yourself that you are actually within Linux and not Windows

## Run an nginx server
nginx is a simple web server and the image that we will be using is the go-to example for simple networking and web hosting using Docker.

1. Run `docker run -p 80:80 nginx`, this starts the server. `-p 80:80` binds port 80 within the container to our host's port 80.
2. Once the server is running, open a browser and go to `localhost:80`
3. On ubuntu, to kill the server, type CTRL+C. On Windows, just close the window.
4. Now, try changing either of the port numbers to `8001` and find out which one controls the host port and which one the container port. Now make sure that you can visit the webserver via `localhost:8001`.
5. Once you are done, make sure no containers are running anymore.
6. Now, remove all stopped containers as well by identifying them via `docker ps -a` and then running `docker rm <container id>`
7. Tip: You can automatically remove containers after they are stopped by adding the `--rm` paramter to `docker run`.

## Run an nginx server pt2
Let's now insert some files into a container

1.  Create a new directory (`mkdir`) somewhere and go into it (`cd`) and create the following two files:
2. `echo "My own 50x page" > 50x.html`
3. Run the server while attaching our current folder (`-v <folder>` stands for "volume"): `docker run -p 80:80 -v "%cd%":/usr/share/nginx/html nginx:latest`
   - If you are on Ubuntu, replace `%cd%` with `$(pwd)`
4. You should now be able to see your served file on `http://localhost/50x.html`
5. Now, a small challenge: Create two nginx servers, one reachable via `localhost:8001` and another one via `localhost:8002`. Start both servers with the `-d` parameter to start them in the background.

## interactive vs detached vs default
1. Run a few containers with the `-it` or `-d` parameters or no parameters. Play around a little bit and try to understand what each of them do.
2. If you have a question about what is happening, please ask.