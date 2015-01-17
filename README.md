# SGT Docker

Here are the steps to setup production SGT environment:

* *username* is your docker username
* *image* is the name of your docker image
* *flag* is the flag of your docker image


## Pulling docker images

First, we need to pull the images for postgres and the ruby on rails web server to our machine:

1. Login to docker hub: `sudo docker login`
1. Pull the postgres image: `sudo docker pull liabasb/sgt-postgres`
1. Pull the rails app image: `sudo docker pull liabasb/sgt`

## Running docker images

### Running the postgres image into a container

1. `sudo docker run --name my-postgresql -e POSTGRES_PASSWORD=mypassword -d postgres`

### Running the rails app image into a container for the first time

1. `sudo docker run -ti --link my-postgresql:postgresql -p 8080:8080 username/image:flag /bin/bash`
2. `rake db:create db:migrate db:populate`
3. `sudo docker run -ti --link my-postgresql:postgresql -p 8080:8080 username/image:flag`

### Running the rails app image into a container when migrations are needed for the database

1. `sudo docker run -ti --link my-postgresql:postgresql -p 8080:8080 username/image:flag /bin/bash`
2. `rake db:migrate`
3. `sudo docker run -ti --link my-postgresql:postgresql -p 8080:8080 username/image:flag`

### Running the rails app image again

1. `sudo docker run -ti --link my-postgresql:postgresql -p 8080:8080 username/image:flag`
2. `sudo docker ps -a`
3. `sudo docker inspect username/image:flag`


## Development

### Updating SGT rails app image:

1. Work on the code; update the app...
2. Build the docker image from this code: `sudo docker build -t username/image .` *(optionnaly set a flag to that image: `sudo docker build -t username/image::flag .`)*
3. Check that the image has been created: `sudo docker images`
3. Check that the new image run properly: *see running images*
4. Push that new image to docker hub: `sudo docker push username/image`
3. Commit: `sudo docker images`
