
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

#### docker-rails-app/Dockerfile

```
# Here we add the the name of the stage ("base")
FROM ruby:3.1.2-slim AS base

# Common dependencies
RUN apt-get update -qq \
  && DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
    build-essential \
    gnupg2 \
    curl \
    less \
    git \
    default-libmysqlclient-dev \
    libsqlite3-dev \
    libedit-dev \
  && apt-get clean \
  && rm -rf /var/cache/apt/archives/* \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
  && truncate -s 0 /var/log/*log

# Install NodeJS and Yarn
ARG NODE_MAJOR=16
RUN curl -sL https://deb.nodesource.com/setup_$NODE_MAJOR.x | bash -
RUN apt-get update -qq && DEBIAN_FRONTEND=noninteractive apt-get -yq dist-upgrade && \
  DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
    nodejs \
    && apt-get clean \
    && rm -rf /var/cache/apt/archives/* \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && truncate -s 0 /var/log/*log
RUN npm install -g yarn

# Create a directory for the app code, bundler, and supporting directories
RUN mkdir -p /app
RUN mkdir -p /bundle

# Set environment variables
ENV LANG=C.UTF-8 \
  BUNDLE_JOBS=4 \
  BUNDLE_RETRY=3 \
  BUNDLE_APP_CONFIG=/bundle \
  BUNDLE_PATH=/bundle \
  GEM_HOME=/bundle \
  RAILS_ENV=development

# Upgrade RubyGems and install the latest Bundler version
RUN gem update --system && \
    gem install bundler

# Install development dependencies from Aptfile.dev
#COPY Aptfile.dev /tmp/Aptfile.dev

RUN apt-get update -qq && DEBIAN_FRONTEND=noninteractive apt-get -yq dist-upgrade && \
  DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
    $(grep -Ev '^\s*#' /tmp/Aptfile.dev | xargs) && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    truncate -s 0 /var/log/*log

WORKDIR /app

# Copy dependency files
COPY Gemfile Gemfile.lock ./

# TODO: Stop forcing platform to Ruby once we're at Ruby >= 2.6
# We do this to be able to install Nokogiri because our image doesn't have
# glibc 2.29 and we cannot install glibc 2.29 on our image.
# With this approach, Nokogiri is installed without C extensions and the performance
# is slower.

# Install Ruby gems and configure Bundler
RUN mkdir -p $BUNDLE_PATH \
  # && bundle config --local deployment 'true' \
  && bundle config --local path "${BUNDLE_PATH}" \
  && bundle config --local with 'development test' \
  && bundle config --local clean 'true' \
  && bundle config --local force_ruby_platform 'true' \
  && bundle config --local no-cache 'false' \
  && bundle install --jobs=${BUNDLE_JOBS} \
  && rm -rf /bundle/cache/*

# Copy code
COPY . .

# Precompile assets
# NOTE: The command may require adding some environment variables (e.g., SECRET_KEY_BASE) if you're not using
# credentials.
# RUN bundle exec rails assets:precompile

# Expose port 3000 to the host
EXPOSE 3000

CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0"]
#CMD ["/bin/bash"]
```
#### Here are some of the instructions we have used in Dockerfile


**FROM** is used to tell Docker to download a public image, which is then used as the base for our image. Here we use an image which contains a specific version of Ruby.

**RUN** is used to execute a command inside the image that we are building. Here we are installing some of the ubuntu libraries which will be used as dependencies.

**COPY** is used to copy any of specific file to the image from the local directories where **Dockerfile** is saved.

**WORKDIR** instruction is used to set the working directory for all the subsequent Dockerfile instructions.

**EXPOSE** is used to open the port.  EXPOSE instruction exposes a particular port with a specified protocol inside a Docker Container. Here we are opening 3000 port to run the rails server. 

**CMD**  command​ specifies the instruction that is to be executed when a Docker container starts.


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

## Running Docker Image
A Docker container is a runtime instance of a Docker image. Images can exist without containers, whereas a container needs to run an image to exist. 

Therefore, containers are dependent on images and use them to construct a run-time environment and run an application. 

Here is the command to run a docker image:

```
docker run -p 3000:3000 mydockerimage/docker-rails-app:latest
```
