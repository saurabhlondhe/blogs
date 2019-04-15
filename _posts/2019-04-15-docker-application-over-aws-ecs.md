---
title:  "Deploying a docker web application using AWS-ECS"
author: "Saurabh Londhe"
avatar: "img/authors/saurabh.jpg"
image: "img/docker-aws.jpg"
date:   2019-04-15
---
### Deploying a docker web application to AWS-ECS
### For those who had just started, we'll have a look at docker and ECS.

Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package. By doing so, thanks to the container, the developer can rest assured that the application will run on any other Linux machine regardless of any customized settings that machine might have that could differ from the machine used for writing and testing the code.
In a way, Docker is a bit like a virtual machine. But unlike a virtual machine, rather than creating a whole virtual operating system, Docker allows applications to use the same Linux kernel as the system that they're running on and only requires applications be shipped with things not already running on the host computer. This gives a significant performance boost and reduces the size of the application.

Amazon Elastic Container Service (Amazon ECS) is a highly scalable, high-performance container orchestration service that supports Docker containers and allows you to easily run and scale containerized applications on AWS. Amazon ECS eliminates the need for you to install and operate your own container orchestration software, manage and scale a cluster of virtual machines, or schedule containers on those virtual machines.

### Creating a docker image

You can create a docker images by using Dockerfile or else you can create an image by configuring existing image manually.
I'll go with existing [httpd](https://hub.docker.com/_/httpd) image and configure it as i want, So let's start.

1.  Login to AWS and go to Services-> ECR, and create a ECR repository

![ecr-image](../img/aws-ecr/1.png)

2.  Give title to repository.
>   this title should be more specific. While downloading this image the same title is used with versions

![repo-name](../img/aws-ecr/2.png)

3.  For command help you can use ```View push commands``` tab, which will include all commands used for uploading an image to your AWS repository

![push-command-help](../img/aws-ecr/3.png)

Popup will apear with some commands as follows

![push-command-popup](../img/aws-ecr/4.png)

4.  Executing first command to login

```sh
aws ecr get-login --no-include-email --region ap-south-1
```

![aws-login](../img/aws-ecr/5.png)

copy the output and execute that command, after that ![login-img](../img/aws-ecr/6.png) message will appear.

5.  Pull image from docker hub or create from ```Dockerfile```. I'll pull httpd from docker hub

```sh
docker pull httpd
```
Now it'll download an image to your local machine and to see it you can also use

```sh
docker images
```
Following will be output of  "```docker images```"
```sh
#   REPOSITORY     TAG        IMAGE ID            CREATED             SIZE
#   httpd          latest     d4a07e6ce470        12 days ago         132MB
```

6.  Take ssh of ```httpd``` image to configure it manually.
![ssh-httpd-image](../img/aws-ecr/ssh-httpd.png)

    update ```/urs/local/apache2/htdocs/index.html``` and change content.

![index.html-file](../img/aws-ecr/7.png)

to save the image with its content it need to be commited. 

![aws-login](../img/aws-ecr/9.png)

-   Fist get container id using ```docker ps``` and use that id to commit your image with the same name of repository that we have created in ECR.

    ```sh
    docker commit 28d64655f452 test-http-server
    ```
-   You can see commited image by executing ```docker images```


![aws-login](../img/aws-ecr/10.png)
![aws-login](../img/aws-ecr/11.png)
![aws-login](../img/aws-ecr/12.png)
![aws-login](../img/aws-ecr/13.png)
![aws-login](../img/aws-ecr/14.png)
![aws-login](../img/aws-ecr/15.png)
![aws-login](../img/aws-ecr/16.png)
![aws-login](../img/aws-ecr/17.png)
![aws-login](../img/aws-ecr/18.png)
![aws-login](../img/aws-ecr/19.png)
![aws-login](../img/aws-ecr/20.png)
![aws-login](../img/aws-ecr/21.png)
![aws-login](../img/aws-ecr/22.png)
![aws-login](../img/aws-ecr/23.png)