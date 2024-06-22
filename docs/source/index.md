# Greetings!

## Welcome to **Annatar Contacts** documentation.

### Table of Contents

1. [Overview](#overview)
2. [Installation](#installation)
3. [Extra Configuration](#extra-configuration)
4. [How to Use](#how-to-use)
5. [Possible Questions](#possible-questions)

### Overview

Annatar Contacts is a simple Docker-built CRUD (Create, Read, Update, and Delete) application designed to store personal data of the people you know.

Through this guide, you will be able to run this application and use it as you find suitable. Notice that some questions may be answered in the [Possible Questions](#possible-questions) section.

### Installation

Clone this repository using the following command:

`git clone https://github.com/FalarzEdu/annatar.git`

Navigate to the project root directory.

The application needs two containers:

- One for the source code
- A second for the database

To set it up, follow these steps:

1. Inside the 'crud' folder, open the 'connection.php' file and change the database container IP. You can also change the user and password, but this is optional.
2. Execute this command to run the app core container:

`docker container run --name {container-name} -d -p 80:80 -p 443:443 -v ./crud:/var/www/html crud:1.2`

3. (This step is not required if you did not change the database credentials in step 1). Inside the 'db' folder, open the 'banco.sql' file and set the user and password in the highlighted lines to the same you wrote in the 'connection.php' file in the first step.
4. Execute this command to start your database:

 `docker run --name {container-name} -d -e POSTGRES_PASSWORD=123 postgres:1.0`

> Note: The password '123' can (and is recommended to) be changed as you like.

5. The build process is done! Now access the application using these DNS:
   1. https://www.anatar.com
   2. https://anatar.com

### Extra Configuration

In this section, we will discuss a little about the extra configurations for the app. They are not essential—at least to run locally. We are talking about DNS and the SSL certificate.

##### DNS (Domain Name System)

The **DNS** is basically a **contact book** used by your browser to check if the typed domain exists and retrieve its IP. To build this project, we used a virtual machine running a **Bind9** server to perform the function of a local **DNS**.

We configured **Bind9** to give the browser the **core app container** IP whenever it searched for the application domains (see [Installation](#installation)). It looks like this:

`$ORIGIN anatar.com.
$TTL 300;
@ IN SOA dns {email@domain.com}. (1 30 30 30 30);
@ IN NS dns
dns IN A {VM IP}
@ IN A {core app container IP}
web IN CNAME @
www IN CNAME @`

##### SSL Certificate

To allow access to our application through the HTTPS protocol, obtaining an SSL certificate is necessary. It is a "virtual document" signed by an authority able to tell your browser that our site has a secure **HTTP** connection.

Considering that we did not intend to use our application publicly, acquiring a real certificate was not mandatory. Instead, we used a free program to generate and sign a certificate so we could "simulate" a real scenario. The program in question is called **easy-rsa**.  

### How to Use

#### Adding Records

1. Click on the **Add Record** button.
2. Fill in the requested information about your new contact.
3. Click **Submit**.
4. Done! The recently added contact will now appear on your list.

#### Updating Records

1. Click on the **Update** button.
2. Change the displayed information as desired.
3. Click on **Update Record**.
4. Done! The data is now updated.

#### Deleting Records

1. Click on the **Delete** button.
2. A window will pop up asking you to confirm the action.
3. Click **OK**.
4. Done! The record was removed.

### Possible Questions

Here is some information that may be important to better understand this document.

##### What do these **{ xxx }** mean?

- We used them to denote variables. In other words, they mean that you must replace them with something else. Example:
  - --name {container-name} ---> --name my-container

##### Is it a problem if I do not change the database credentials?

- Well, it depends. As long as you run this application locally, not so much. However, if you manage to use this CRUD on the World Wide Web, everyone will have access to your database if they read this tutorial. In summary, we strongly recommend that you change the DB credentials.

##### Am I free to use this app as I want?

- Yes. Enjoy it as much as you can.
