# otrs-daemon

OTRS daemon docker container based on Alpine Linux.

This container runs the OTRS daemon via crond as recommended by OTRS A.G. The daemon is a forking Perl process that is responsible for all scheduled actions in OTRS, such as importing email, sending email, removing expired sessions, escalating tickets, etc. It is not required for a functioning OTRS web interface, but is required for all other aspects.

## How to deploy

Please see my main [otrs-docker][1] repository for full instructions and the docker-compose file that automates the deployment of these images.

If you would like to run this image manually for testing purposes, then this docker run command will start it in the same way as the docker-compose file:
```
docker run -dt --restart unless-stopped --name otrs-daemon --mount source=otrs-config,target=/data --mount source=otrs-dir,target=/opt/otrs --network otrs-backend snw35/otrs-daemon:latest
```
Note that the OTRS daemon will not be able to run without a configured and installed OTRS system with a functional database and web frontend.

## About my images

All of my containers follow these main guidelines:

 * __Follow best practice.__ Adhere as closely as possible to the [official docker library image guidelines.](https://github.com/docker-library/official-images)
 * __No version-dependent scripts.__ No custom scripts or glue code that would need to be updated alongside the hosted application.
 * __Small and simple.__ Based on official Alpine Linux with as minimal Dockerfiles and images as possible.
 * __One process, one container.__ No process supervisor daemons or hacks. Allow the container runtime to have full visibility of each running process.
 * __Disposable and immutable.__ Strict separation of user and application data means that any container can be stopped and replaced without affecting the configuration state of the application.
 * __Security focused.__ No docker socket bind mounts, ever. All processes are run by a dedicated application user with minimal permissions where possible.
 * __True to the application.__ The application's defaults are not altered in any way, and no additions or subtractions are made to functionality.
If you like these guidelines, then please check out my other images here or on Dockerhub.

[1]: https://github.com/snw35/otrs-docker


***

 * [Travis CI: ![Build Status](https://travis-ci.org/snw35/otrs-daemon.svg?branch=master)](https://travis-ci.org/snw35/otrs-daemon)
