# How to setup telegraf, influxdb and grafana using docker-compose.
In order to setup the TIG monitoring stack using [ docker compose](https://docs.docker.com/compose/install/ "docker-compose") , first of all, you have to make sure that you have the latest version installed on your docker machine. Then you can then begin to write you [docker compose file](https://github.com/Osaschrist/TIG-stack/blob/main/docker-compose-arm.yml "docker compose file for arm architecture") which will contain the tree tools we are going to use.

**NOTE:** When selecting an image for your container you need to take note of the architecture because in some cases, you will have to indicate it using the the following:
 `platform: linux/amd64`

## Telegraf configuration file (telegraf.conf)
You can define your telegraf initial configuration outside of you telegraf container and in order to do so, you have to add the following line in your docker compose file:
` volumes:`</br>
      `- ./telegraf.conf:/etc/telegraf/telegraf.conf:ro` <br>
## .ENV file
A .env file or dotenv file is a simple text configuration file for controlling your Applications environment constants. Between Local, Staging and Production environments, the majority of your Application will not change. However in many Applications there are instances in which some configuration will need to be altered between environments. Common configuration changes between environments may include, but not limited to, URL's and API keys. Here you can find the example of how it was applied.

```bash
$cat .env
#Influxdb Variables
MODE=setup
USERNAME=admin
PASSWORD=P@ssw0rd
```
```bash
$cat docker-compose.yml
 environment:
      - DOCKER_INFLUXDB_INIT_MODE=${MODE}
      - DOCKER_INFLUXDB_INIT_USERNAME=${USERNAME}
      - DOCKER_INFLUXDB_INIT_PASSWORD=${PASSWORD}
```
After making all the neccessary configurations, you can then spin up your docker compose file with the `docker-compose up - d` command.
 Or with this command ` docker-compose --env-file .env -f docker-compose-arm.yml up -d` <br/>

 Where `-f ` is used to indicate the docker compose file to spin up and `--env-file` to indicate you .env file. But it only useful if you change the standard name of both file.

 ### **It is a good practice to use the this `docker-compose --env-file .env -f docker-compose-arm.yml config` command to check if you `.env` file configuration is correct**
 
