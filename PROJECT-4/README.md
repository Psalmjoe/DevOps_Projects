# LEMP STACK IMPLEMENTATION

## Introduction


LEMP refers to a collection of open-source software that is commonly used together to serve web applications. The term LEMP is an acronym that represents the configuration of a Linux operating system with an nginx (pronounced engine-x, hence the E in the acronym) web server, with site data stored in a MySQL database and dynamic content processed by PHP.

This guide demonstrates how to install a LEMP stack on an Ubuntu 20.04 server. The Ubuntu operating system takes care of the first requirement. We will describe how to get the rest of the components up and running.

## Prerequisites

In order to complete this project, you will need an AWS account and a virtual server with an Ubuntu server OS.

If you do not have an AWS account, to back to project 3 (LAMP STACK IMPLEMENTATION) to sign in to an AWS free tier account and create an EC2 account with Ubuntu server 22.04 LTS (HVM) image.

After downloading and installing Git Bash, lauch it and run the below command :

```ssh -i <Your-private-key.pem>ubuntu@<EC2-Public-IP-address>```

![Alt text](images/ssh.png)

## Installing the Nginx Webserver

### Step 1 - Installing the Nginx Webserver

In order to display web pages to our site visitors, we are going to employ Nginx, a high-performance web server. We’ll use the apt package manager to obtain this software.

Since this is our first time using apt for this session, start off by updating your server’s package index. Following that, you can use apt install to get Nginx installed:

```sudo apt update```

```sudo apt install nginx```

When prompted, enter Y to confirm that you want to install Nginx. Once the installation is finished, the Nginx web server will be active and running on your Ubuntu 20.04 server.

To verify that Nginx was successfully installed and is running as a service in Ubuntu, run :

```sudo systemctl status nginx```

![Alt text](<images/nginx status.png>)

If it is green and running as above then you did everything correctly and have just lauched your webserver in he cloud.

Before we can receive any traffic by our webserver, we need to open TCP port 80 which is the default port that web browsers use to access web pages on the internet. Up until now only the SSH port 22 is open by default during our instance launch.

Port 80 can be opened by modifying the security group of the running EC2 instance.

![Alt text](<images/sec group.png>)

![Alt text](<images/sec group edit.png>)

![Alt text](<images/inbound rule.png>)

Our server is now running and we can access it both locally and on the internet from any Ip.

First, let us try to access it locally in our Ubuntu shell. Run :

```curl http://localhost:80```

or

```curl http://127.0.0.1:80```

![Alt text](<images/curl hostname.png>)

The 2 commands above are the same. The difference is that the first one uses the DNS name while the second uses the local IP which corresponds to the DNS name, localhost.

Next, we can test if our Nginx HTTP server can respond to requests from the internet. Open any browser and try to access the url below :

```http://<Public-IP-Address>:80```

Another way to retrieve your public Ip address other than to check it in AWS console is to run the below command :

```curl -s http://169.254.169.254/latest/meta-data/public-ipv4```

Since all browsers use port 80 by default, it is not neccessary to specify the port number.

If you can see the below page, it means that you have correctly installed your Apache web server and accessible through your firewall.

![Alt text](images/nginx.png)

The above is the same result we got using the curl command but now represented in nice HTML format by the web browser.

## Installing Mysql
### Step 2 - Installing Mysql

Now that our webserver is up and running, we need to install a Database Management System (DBMS) to be able to store and manage data for our site. For this purpose, we will use Mysql, a relational database managemet system used within PHP environments.

To install Mysql-server, run the code below :

```sudo apt install mysql-server```

When prompted, confirm the installation by typing y and the press enter.

![Alt text](<images/msql install.png>)

When installation is completed, log in to mysql console using the command :

```sudo mysql```

This will connect to the administrative database user root and you will see an output as below :

![Alt text](<images/sudo mysql.png>)

It is recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system.

Before running the script, you will set a password for the root user using mysql_native_password as default authentication method. We are defining this user's password as PassWord.1

```ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';```

![Alt text](images/mysql-password.png)

After making this change, exit the MySQL prompt:

```mysql> exit```

![Alt text](<images/exit mysql.png>)

Following that, you can run the mysql_secure_installation script without issue.

Start the interactive script by running:

```sudo mysql_secure_installation```

This will ask if you want to configure the VALIDATE PASSWORD PLUGIN.

Note: Enabling this feature is something of a judgment call. If enabled, passwords which don’t match the specified criteria will be rejected by MySQL with an error. It is safe to leave validation disabled, but you should always use strong, unique passwords for database credentials.

Answer Y for yes, or anything else to continue without enabling.

VALIDATE PASSWORD PLUGIN can be used to test passwords and improve security. It checks the strength of password and allows the users to set only those passwords which are secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:

If you answer “yes”, you’ll be asked to select a level of password validation. Keep in mind that if you enter 2 for the strongest level, you will receive errors when attempting to set any password which does not contain numbers, upper and lowercase letters, and special characters:

![Alt text](<images/edit pass.png>)

Regardless of whether you chose to set up the VALIDATE PASSWORD PLUGIN, your server will next ask you to select and confirm a password for the MySQL root user. This is not to be confused with the system root. The database root user is an administrative user with full privileges over the database system. Even though the default authentication method for the MySQL root user doesn’t involve using a password, even when one is set, you should define a strong password here as an additional safety measure.

If you enabled password validation, you’ll be shown the password strength for the root password you just entered and your server will ask if you want to continue with that password. If you are happy with your current password, enter Y for “yes” at the prompt:

![Alt text](<images/new pass.png>)

For the rest of the questions, press Y and hit the ENTER key at each prompt. This will remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes you have made.

![Alt text](<images/mysql setup.png>)

When you’re finished, test whether you’re able to log in to the MySQL console by typing:

```sudo mysql -p```

Notice the -p flag in this command which will prompt you for the command used after chaning the root user password.

To exit the Mysql console, type :

```mysql> exit```

![Alt text](<images/mysql -p.png>)

For increased security, it’s best to have dedicated user accounts with less expansive privileges set up for every database, especially if you plan on having multiple databases hosted on your server.

Note: At the time of this writing, the native MySQL PHP library mysqlnd doesn’t support caching_sha2_authentication, the default authentication method for MySQL 8. For that reason, when creating database users for PHP applications on MySQL 8, you’ll need to make sure they’re configured to use mysql_native_password instead. We’ll demonstrate how to do that in Step 6.

Your MySQL server is now installed and secured. Next, you’ll install PHP, the final component in the LEMP stack.

## Installing PHP
### Step 3 - Installing PHP

You have Nginx installed to serve your content and MySQL installed to store and manage your data. Now you can install PHP to process code and generate dynamic content for the web server.

While Apache embeds the PHP interpreter in each request, Nginx requires an external program to handle PHP processing and act as a bridge between the PHP interpreter itself and the web server. This allows for a better overall performance in most PHP-based websites, but it requires additional configuration. You’ll need to install php-fpm, which stands for “PHP fastCGI process manager”, and tell Nginx to pass PHP requests to this software for processing. Additionally, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. Core PHP packages will automatically be installed as dependencies.

To install the php-fpm and php-mysql packages, run :

```sudo apt install php-fpm php-mysql```

When prompted, type Y and ENTER to confirm installation.

![Alt text](<images/php install.png>)

You now have your PHP components installed. Next, you’ll configure Nginx to use them.