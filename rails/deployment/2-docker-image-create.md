# Running application using docker container

In this section we will setup docker configuration to run the rails project in docker container.

Assuming we already have installed a basic dependencies in the machine like Ruby on Rails, Git, Docker, etc.


## Rails application setup
Initially we have to create a basic rails application which we will run through docker or we can use any of existing rails app.

Here we are creating a new rails application

`rails new docker-rails-app`

Now we are creating a landing page via welcome controller and setting root path for this action.
Assuming we are done with this step.

**config/routes.rb**

**app/controllers/welcome_controller.rb**

    class WelcomeController < ApplicationController
        def index
        end
    end
Add some content to view file

*app/views/welcome/index.html.erb*

Here we are using sqlite for the database. We can use MySQL, Postgresql, etc as per our requirement.

## Docker image

A Docker image is a file used to execute code in a Docker container. Docker images act as a set of instructions to build a Docker container, like a template. 

A Docker image is a package which contains our application with all the dependencies and system libraries needed to run it.

Docker images also act as the starting point when using Docker. An image is comparable to a snapshot in virtual machine (VM) environments.

We have already installed docker in the machine.

*Go to your root directory of the application and create a new file with name **Dockerfile***

### Dockerfile
A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. 
- [Check here to create a Dockerfile](https://github.com/TecOrb-Developers/handbook/blob/main/rails/deployment/1-Dockerfile.md)


## Building Image

Above we added all the dependencies and instructions to build the image in Dockerfile. This is the time to build the image.

Below is the command to build the image:
```
  docker build -t mydockerimage/docker-rails-app:latest .
```
**Note:**

- **-t** is used to assign a name and a tag to the new image. This makes it easier to find the image later. We can also use a repository name as the image name.

- **The image name** is the part **before the colon** (*mydockerimage/docker-rails-app*)

- **Tag** is the part **after the colon** (*latest*). We can also ignore the tag *latest* since it is the default value used in case the tag is omitted

- **Dot (.)** is a required argument and indicates the path to the Dockerfile.

By executing above command our image will be build successfully. We can see the list of all docker images in our system by below command:

```
docker image ls
```
We can see a list like:
| REPOSITORY                      | TAG     | IMAGE ID      | CREATED       | SIZE  |
| :------------------------------ | :-------| :------------ | :------------ |:----- |
| mydockerimage/docker-rails-app  |  latest | 0e4e616f7b52  | 1 minute ago  | 554 MB |


### Here is a sample project created for the same:
- [Build Docker image Rails](https://github.com/TecOrb-Developers/rails-docker-image)