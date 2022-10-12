## Running Docker Image
A Docker container is a runtime instance of a Docker image. Images can exist without containers, whereas a container needs to run an image to exist. 

Therefore, containers are dependent on images and use them to construct a run-time environment and run an application. 

Here is the command to run a docker image:

```
docker run -p 3000:3000 mydockerimage/docker-rails-app:latest
```

**Note**
- Left hand 3000 port is host port. 
- Right hand 3000 port is container port. 
- We can also use other ports in case. If we change the container port, we also need to update the image to make sure that the Rails server listens on the correct port.
- We also need to open that port using EXPOSE in case we are changing the container port.

Now https://localhost:3000 is serving our rails application.

### Here is a sample project created for the same:
- [Build Docker image Rails](https://github.com/TecOrb-Developers/rails-docker-image)