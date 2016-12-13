---
description: Deploy the app as a Docker Cloud service
keywords: Python, deploy, Cloud
redirect_from:
- /docker-cloud/getting-started/python/5_deploy_the_app_as_a_service/
- /docker-cloud/getting-started/golang/5_deploy_the_app_as_a_service/
title: Deploy the app as a Docker Cloud service
---

In this step you will deploy the app as a Docker Cloud Service. Remember that a service is a group of containers of the same **image:tag**.

What you'll do in this step is slightly different if you have Docker Engine
installed locally or not.

* If you have Docker Engine installed locally, start at
[Deploy app with Docker Engine installed locally](5_deploy_the_app_as_a_service.md#deploy-app-with-docker-engine-installed-locally).

* If you do not have Docker Engine installed locally, start at [Deploy app without Docker Engine installed locally](5_deploy_the_app_as_a_service.md#deploy-app-without-docker-engine-installed-locally).


## Deploy app with Docker Engine installed locally

Start by running the service.

```bash
$ docker-cloud service run -p 80 --name web $DOCKER_ID_USER/quickstart-python
```

or

```bash
$ docker-cloud service run -p 80 --name web $DOCKER_ID_USER/quickstart-go
```

Skip the next section and read about [The run command](5_deploy_the_app_as_a_service.md#the-run-command).

## Deploy app without Docker Engine installed locally

If you don't have Docker Engine installed locally and you have been following
this tutorial, you probably don't have either of the quickstart images in your
private registry in Docker Cloud. To deploy the service without Engine installed
locally, use the public images `dockercloud/quickstart-python` or
`dockercloud/quickstart-go` available on Docker Hub.

To do this execute one of the following commands:

**Python quickstart**

```bash
$ docker-cloud service run -p 80 --name web dockercloud/quickstart-python
```

**Go quickstart**

```bash
$ docker-cloud service run -p 80 --name web dockercloud/quickstart-go
```

Go to the next section to read about [The run command](5_deploy_the_app_as_a_service.md#the-run-command).

## The run command

The `run` command **creates and runs** the service using the image you chose. The **-p 80** flag publishes port 80 in the container so that it is publicly accessible, and maps it to a dynamically assigned port in the node.

It might take a minute or two to get your service up and running. Once it
completes the startup process, it will be in the *running* state.

To check the status of your service from the CLI use the `docker-cloud service ps` command.

```none
$ docker-cloud service ps
NAME                 UUID      STATUS     IMAGE                                          DEPLOYED
web                  68a6fb2c  ▶ Running  my-username/quickstart-python:latest           1 hour ago
```

Make sure that the **STATUS** for your service is **Running**. Next, visit the
app at the URL generated by its service name. Find this URL by running
`docker-cloud container ps`.

```none
$ docker-cloud container ps
NAME                   UUID      STATUS     IMAGE                                          RUN COMMAND          EXIT CODE  DEPLOYED      PORTS
web-1                  6c89f20e  ▶ Running  my-username/quickstart-python:latest           python app.py                   1 minute ago  web-1.my-username.cont.dockerapp.io:49162->80/tcp
```

The **PORTS** column contains the URL you can use to see the service running in
a browser. Copy the URL, open a browser, and go to that URL. In the example above, the URL is
`web-1.my-username.cont.dockerapp.io:49162`.

If you don't want to leave the command line, you can use the `curl` command instead.

```bash
$ curl web-1.$DOCKER_ID_USER.cont.dockerapp.io:49162
Hello World!</br>Hostname: web-1</br>Counter: Redis Cache not found, counter disabled.%
```
> **Tip**: Your Docker ID is used as part of the namespace when running containers in Docker Cloud. In the example above, instead of copying the URL entirely, you can see we used the $DOCKER_ID_USER variable.

**CONGRATULATIONS!** You've deployed your first service using Docker Cloud.

Next: [Define environment variables](6_define_environment_variables.md).