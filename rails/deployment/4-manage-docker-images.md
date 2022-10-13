## Docker images management locally

Here is the complete [documentation to manage the docker images](https://docs.docker.com/engine/reference/commandline/image/). Here are some of the major commands we will use to manage the images

### We can see the list of all docker images in our system by below command:

```
docker image ls
```

We can see a list like:
| REPOSITORY                      | TAG     | IMAGE ID      | CREATED       | SIZE  |
| :------------------------------ | :-------| :------------ | :------------ |:----- |
| mydockerimage/docker-rails-app  |  latest | 0e4e616f7b52  | 1 minute ago  | 554 MB |


### We can delete image:

```
docker image rm [OPTIONS] IMAGE [IMAGE...]
```

Options: `--force`, `-f`

Here is an example to delete above image:

```
docker image rm -f mydockerimage/docker-rails-app:latest
```

### We can pull image:

```
docker image pull [OPTIONS] NAME[:TAG|@DIGEST]
```

Options: `--all-tags` , `-a`, `--platform`, `--quiet`, `-q`


### Login docker account on terminal

Use your dockerhub username and password to login on terminal

```
docker login
```

### For more uses please visit the [Docker main documentation](https://docs.docker.com/reference/)
- [Commandline Image](https://docs.docker.com/engine/reference/commandline/image/).
- [Commandline CLI](https://docs.docker.com/engine/reference/commandline/cli/)