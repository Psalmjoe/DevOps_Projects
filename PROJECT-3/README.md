# LAMP STACK IMPLIMENTATION

A technology stack is a set of frameworks and tools used to develop a software product. It is essentially a set of technologies that are stacked together to build any application. Popularly known as a technology infrastructure or solutions stack, technology stack has become essential for building easy-to-maintain, scalable web applications.

Technology stack determines the type of applications you can build, the level of customizations you can perform, and the resources you need to develop your application. A technology stack consists of two primary components: a frontend stack and a backend stack. Some popular examples of tech stack include:

* The LAMP stack: Linux, Apache, MYDQL and PHP,
* LEMP stack: Nginx, MYSQL and PHP
* MEAN stack: MongoDB, Express.js AngularJS and Node.js.
* MERN stack: MongoDB, Express.js, React, and Node.js.

## Preparing Prerequisite

To complete this tutorial, you will need an AWS account and a virtual server with Ubuntu OS.

Click on the below links to watch a video on how to :

1. [_Setup your account and provision an ubuntu server with EC2_](https://www.youtube.com/watch?v=xxKuB9kJoYM&list=PLtPuNR8I4TvkwU7Zu0l0G_uwtSUXLckvh&index=7)

2. [_Connect to your EC2 instance_](https://www.youtube.com/watch?v=TxT6PNJts-s&list=PLtPuNR8I4TvkwU7Zu0l0G_uwtSUXLckvh&index=8)

Alternatively, you can follow the step by step guide below :

1. Register a new AWS account: [Create a new AWS Account](https://portal.aws.amazon.com/billing/signup?nc2=h_ct&src=header_signup&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start/email)

2. Select your prefered region, name your EC2 instance, Create a new key pair, and then launch your EC2 instance (choose t2.micro and ubuntu server 20.04 LTS)

![Alt text](<images/instance name.png>)

![Alt text](<images/machine type.png>)

![Alt text](images/keypair.png)

3. There are different ways to connect to your EC2 instance but in this tutorial, we will use Git bash. Therefore, launch git and change to the directory where the key pair is downloaded (usually the downloads folder or any folder you choose to copy the key pair to. In my case, I have my key pair copied into a folder called <font colour="red"> Devops_linux </font> ) using the below command :

> cd Devops_linux
