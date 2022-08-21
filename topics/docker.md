# Docker

- _Images_: The file system and configuration of the app which r used to create contains. To find out more about a Docker image, run `docker inspect IMAGE`.
- _Containers_: Running instances of the images -- containers run the actual app. A container includes an app and all of its dependencies... u create a container using `docker run`...
- _Docker daemon_: The background service running on the host that manages building, running and distributing the containers.
- _Docker client_: The CL tool that allows the user to interact with the daemon.
- _Docker store_: A registry of images, where u can find trusted and enterprise ready containers, plugins, and Docker editors.

---

- `docker images` show a list of all images on ur system (TAG in results refers a particular snapshot of the image)
- `docker ps -a(--all)` shows all containers
- `docker stop container_id`
- `docker rm CONTAINER`
- `docker pull ubuntu 12.04` When not providing a specific version number, the client defaults to the latest.
- `docker search`
- `docker run [options] image [command] [arg...]`

`docker run alpine ls -l` what happened?

1. The Docker client contacts the Docker daemon
2. The Docker daemon checks local store if the image is available
   locally, and if not, download it from the Docker Store.
3. The Docker daemon creates the container and then runs a command in that container
4. The Docker daemon streams the output of the command to the Docker client

`docker run -it alpine /bin/sh`, with `-i -t` option, it attaches an interactive tty in the container. Then u can run as many commands in the container as u want.

> On my pc the above command gives _the input device is not a TTY_, then prepend the command with `winpty` giving `runtime create failed ... no such file ...`. just use powershell. [check this](https://stackoverflow.com/a/56922783/11844003) and [this](https://stackoverflow.com/a/48623403/11844003)

---

A Dockerfile is a text file that contains a list of commands
that the Docker daemon calls while creating an image. It contains all the info that Docker needs to know to run the app:

- a base Docker image to run from
- location of the project code
- any dependencies it has
- and what commands to run at start-up

`docker build -t <username>/myfirstapp .` create a docker image from a Dockerfile.

- It takes an optional tag name with `-t` flag, and the location of the directory containing the `Dockerfile`
- the `.` indicates the current directory

`docker build -t ass/hole .` (build using `Dockerfile` under the current directory)

`docker run -p ip:container_ip ass/hole` run in a new container (publish [`--expose`] container's port to the host)

#### helping links

[should each image contain a jdk?](https://stackoverflow.com/questions/52849139/should-each-docker-image-contain-a-jdk)

[reddit - run multi containers using the same base image](https://www.reddit.com/r/docker/comments/kqd1ef/if_you_run_multiple_containers_of_the_same_image/)

[user manual](https://docs.docker.com/desktop/windows/)

[commandline reference](https://docs.docker.com/engine/reference/commandline/)
