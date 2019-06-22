## Linux Server Configuration
This project is part of the series of the Full Stack NanoDegree program offered by Udacity.
In this project, the main task is to take a baseline installation of a Linux server and prepare it to host a web application. Also to secure the server from a number of attack vectors, install and configure a database server, and deploy a previuos project called the **Item Catalog**.
The Linux machine used is an **AWS Lightsail VM Ubuntu v16**. Language used for the project is **Python v3**, and database module used is **postgresql** to connect to the database.

### Project Details:
##### Connecting to the server
- The IP address of the server is: `13.229.66.111`
- The SSH port used to login is: `Port 2200`
- The username given for reviewing purposes: `grader`
- Sample command to login to the server: `ssh -i ~/PrivateKey -p 2200 grader@13.229.66.111`

##### Viewing the application
The URL for the hosted Item Catalog web application is:
http://ec2-13-229-66-111.ap-southeast-1.compute.amazonaws.com/

##### Software and configuration
This section will list down the steps taken to complete the server configuration along with required softwares installed.
1. Change the SSH port from 22 to 2200
2. Configure the server to allow only key-based SSH authentication
3. Configure the Uncomplicated Firewall (ufw) to allow connections for SSH port 2200, HTTP port 80 and NTP port 123
4. Create a new user account called `grader` and give it permission to `sudo`
5. Create an SSH key-pair for `grader` using the `ssh-keygen` tool
6. Add the generated public key to the file **/home/grader/.ssh/authorized_keys**
7. Configure the timezone of the server to UTC using `sudo dpkg-reconfigure tzdata`
8. Update and upgrade the packages in the server using `sudo apt-get update` and `sudo apt-get upgrade`
9. Install Apache `sudo apt-get install apache2`
10. Install mod_wsgi for python 3 `sudo apt-get install python-setuptools python-dev libapache2-mod-wsgi-py3`
11. Enable the wsgi mode `sudo a2enmod wsgi`
12. Restart the apache service `sudo service apache2 restart`
13. . Install git and clone the item catalog project `sudo apt-get install git`, `git clone https://github.com/naserenho/CatalogApp.git`
14. Create a directory **/var/www/FlaskApp/FlaskApp** and copy the content of the CatalogApp inside the second FlaskApp
15. Change the **application.py** to **\_\_init\_\_.py** and make it run without a port
16. Install pip3 `sudo apt-get install python-pip3`
17. Install virutalenv `sudo pip3 install virutalenv`
18. Create and activate virutalenv `sudo virtualenv venv`, `source venv/bin/activate`
19. Install Flask then deactivate venv `pip3 install Flask`, `deactivate`
20. Create a virutal host config file `sudo nano /etc/apache2/sites-available/FlaskApp.conf` and fill it according to [here](https://github.com/stueken/FSND-P5_Linux-Server-Configuration) step 11.2 number 17
21. Enable the virtual host `sudo a2ensite FlaskApp`
22. Create the .wsgi File according to [here](https://github.com/stueken/FSND-P5_Linux-Server-Configuration) and Restart Apache `sudo service apache2 restart`
23. Install PostgreSQL `sudo apt-get install postgresql postgresql-contrib`
24. Configure the DB code in the item catalog project to be as `create_engine('postgresql://catalog:PW-FOR-DB@localhost/catalog')` where the password is set accordingly
25. Create a postgre user named catalog dedicated for this DB and has limited permissions, and configure the password to be the same one used inside the application
26. Restart apache and then run the project
27. Check the error log in **/var/log/apache2/error.log** and download every missing package for the application to run using `pip3 install pacakagename`
28. Enable Google Authentication to work by going to the google developers console, choosing the application used for OAuth and adding the necessary urls to Authorised JavaScript origins and Authorised redirect URIs

##### Resources
- https://github.com/stueken/FSND-P5_Linux-Server-Configuration
- https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
- https://www.a2hosting.com/kb/developer-corner/postgresql/managing-postgresql-databases-and-users-from-the-command-line
- https://askubuntu.com/questions/138423/how-do-i-change-my-timezone-to-utc-gmt

### Author
Abdulrahim Naser Eddin, FullStack Nanodegree Cohort 4 of 1mac initiative