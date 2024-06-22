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