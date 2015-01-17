# SGT Docker

Here are the steps to setup production SGT environment:

## Pulling docker images

First, we need to pull the images for postgres and the ruby on rails web server to our machine:

## Running docker images

### Running the postgres image into a container

`sudo docker run --name my-postgresql -e POSTGRES_PASSWORD=mypassword -d postgres`
`sudo docker run -ti --link my-postgresql:postgresql -p 8080:8080 liabasb/sgt /bin/bash`
`rake db:create db:migrate db:populate`
`sudo docker run -ti --link my-postgresql:postgresql -p 8080:8080 liabasb/sgt`
`sudo docker ps -a`
`sudo docker inspect liabasb/sgt:latest`


## Development

### Updating SGT rails app image:

1. Work on the code; update the app...
2. Build the docker image from this code: `sudo docker build -t liabasb/sgt .` *(optionnaly set a flag to that image: `sudo docker build -t liabasb/sgt:stable .`)*
3. Check that the image has been created: `sudo docker images`
3. Check that the new image run properly: *see running images*
4. Push that new image to docker hub:
3. Commit: `sudo docker images`
