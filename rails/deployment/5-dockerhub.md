## Push docker image to Docker Hub

Docker Hub repositories allow you share container images with your team, customers, or the Docker community at large.

- Docker images are pushed to Docker Hub through the `docker push` command. 
- A single Docker Hub repository can hold many Docker images
- Here is the complete [Docker Hub documentation](https://docs.docker.com/docker-hub/repos/) related to create and manage reposetories

### Pushing a Docker container image to Docker Hub

To push an image to Docker Hub, 

- You must first name your local image using your Docker Hub username and the repository name that you created through Docker Hub on the web.
- You can add multiple images to a repository by adding a specific `:<tag>` to them (for example docs/base:testing). If it’s not specified, the tag defaults to latest.
- Name your local images using one of these methods:

	- When you build them, using `docker build -t <hub-user>/<repo-name>[:<tag>]`
	- By re-tagging an existing local image `docker tag <existing-image> <hub-user>/<repo-name>[:<tag>]`
	- By using `docker commit <existing-container> <hub-user>/<repo-name>[:<tag>]` to commit changes
	- Now you can push this repository to the registry designated by its name or tag.

- Now you can push this repository to the registry designated by its name or tag.
	- `docker push <hub-user>/<repo-name>:<tag>`
