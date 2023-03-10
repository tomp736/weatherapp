# Weatherapp

## Prerequisites

* An [openweathermap](http://openweathermap.org/) API key.

### Docker

**Dockerfile**'s have been added to the *frontend* and the *backend* directories to run them virtually on any environment having [docker](https://www.docker.com/) installed. It should work by saying e.g. `docker build -t weatherapp_backend . && docker run --rm -i -p 9000:9000 --name weatherapp_backend -t weatherapp_backend`. If it doesn't, remember to check your api key first. Dont forget to specify the apikey argument as well.

## Docker Compose

This docker compose files requires a dev.env file crated in `~/.weatherapp/dev.env` with api key defined.

``` env
APPID=<api key>
```

### docker-compose.yml

A **docker-compose.yml** file has been added connecting the frontend and the backend, enabling running the app in a connected set of containers. 

```sh
docker-compose -f docker-compose.yaml up
```
### docker-compose-dev.yml

An additional **docker-compose-dev.yml** file also exists to enable local development using containers. 

```sh
docker-compose -f docker-compose-dev.yaml up
```

### Cloud

The weatherapp deployment is managed by the external repository [weatherapp-infra](https://github.com/tomp736/weatherapp-infra) project. When making changes in this repository, the application will be automatically deployed by issuing a repository dispatch using this [workflow file](on_wfc_dispatch_deploy.yml).

|github event|branch|azure-url|frontend|backend|
|---|---|---|---|---|
|push|main|weatherapp-main-vm.westeurope.cloudapp.azure.com|:8000|:9000/api/weather|
|pull request|main-promotion|weatherapp-main-promotion-vm.westeurope.cloudapp.azure.com|:8000|:9000/api/weather|
|push|dev|weatherapp-dev-vm.westeurope.cloudapp.azure.com|:8000|:9000/api/weather|
|pull request|dev-promotion|weatherapp-dev-promotion-vm.westeurope.cloudapp.azure.com|:8000|:9000/api/weather|
