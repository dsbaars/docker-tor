# Tor as a Docker container


![Version](https://img.shields.io/github/v/release/dsbaars/docker-tor?sort=semver) 
![Docker Pulls Count](https://img.shields.io/docker/pulls/dsbaars/tor.svg?style=flat)

Tor service as a docker container, supporting both ARM64 and AMD64 architectures (arm64, amd64).

## Usage instructions

### Environment Variables

> **Note** In order to trigger builds This repository uses the following environment variables:

* `DOCKER_HUB_USER` - the username for docker hub
* `DOCKER_USERNAME` - The username for dockerhub.
* `DOCKER_PASSWORD` - The password for dockerhub
* `DOCKER_TOKEN` - the token for docker hub which can push to this projecta (not used currently)
* `GITHUB_TOKEN` - The token of the current user (this is added automatically)
* `GITHUB_ACTOR` - The user to login to docker.pkg.github.com
* `GITHUB_REPOSITORY` - The repository pathname (used for the push to githubs package registry)
* `MAINTAINER_USER` - This is for utilizing the github container registry
* `MAINTAINER_TOKEN` - This is for utilizing the github container registry

## Running

> this assumes `0.4.7.8` version. But you can substitute this for others

### Command Line

To run this from the command line you would need to create an example [config file](https://github.com/torproject/tor/blob/master/src/config/torrc.sample.in) or use the [cut down config file](https://raw.githubusercontent.com/dsbaars/docker-tor/master/torrc-dist) in this repo.

Then you would need to run:

```bash
docker run --rm -d \
            --network host \
            --name tor \
            -v $PWD/data:/etc/tor \
            -v $PWD/data:/var/lib/tor \
            -v $PWD/run:/var/run/tor \
            dsbaars/tor:0.4.7.8

```
This assumes you have a directory called `data` and a directory called `run` in the current `$PWD`. And the config file `torrc` should live in data.

### Docker-compose

For your convenience, we have a [docker-compose](https://github.com/dsbaars/docker-tor/blob/master/docker-compose.yml-dist) file available for you to use too.

By default this uses host networking and requires `data` and `run` folders to be created and with a [valid torrc file](https://github.com/torproject/tor/blob/master/src/config/torrc.sample.in) 

### Generating Tor Passwords

```bash
docker run --rm \
            --name tor \
            dsbaars/tor:0.4.7.8 \
            --hash-password passwordtogenerate
```
