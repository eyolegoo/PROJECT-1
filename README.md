## PROJECT-1: LAMP STACK IMPLEMENTATION DOCUMENTATION


***STEP 1: INSTALLING APACHE AND UPDATING THE FIREWALL***

- I updated the Ubuntu virtual machine using `sudo apt update`

<img width="819" alt="sudo apt update" src="https://user-images.githubusercontent.com/115954100/208168023-12214529-d411-492e-b39a-7d7186eb26a2.PNG">

- I installed Apache2 using `sudo apt install apache2` and I verified if apache2 is running as a service in the OS using, `sudo systemctl stutus apache2`

<img width="769" alt="Apache2 installed and running" src="https://user-images.githubusercontent.com/115954100/208168253-63373b52-acb9-4ba0-ab55-a554eb66f76f.PNG">

- Afterwards, I added a rule to my EC2 configuration to open inbound connection through port 80.

- I accessed my apache web server locally on my ubuntu shell with a hostname and with an IP address using the command code `curl http://localhost:80`  and `curl http://127.0.0.1:80` respectively.

<img width="953" alt="Accessing web server locally using Ubuntu shell run" src="https://user-images.githubusercontent.com/115954100/208168706-1c12b28f-2b58-4e61-b562-1b6195d8d456.PNG">

- Finally, I tested the apache web server on the internet using `http://<Public-IP-Address>:80`

<img width="947" alt="Apache HTTP server responding to request from the internet" src="https://user-images.githubusercontent.com/115954100/208168966-55d95b86-1f59-449b-b71a-6305d986ae23.PNG">


***STEP 2: INSTALLING MY MYSQL***

- My web server is up and running. A DBMS is needed for data storage and management for my web server. So I installed MYSQL for this purpose using the code `sudo apt install mysql-server`

<img width="868" alt="INSTALLED MySQL" src="https://user-images.githubusercontent.com/115954100/208170424-69a36c89-421e-4d68-b206-95587b2d3114.PNG">

- Then I logged on my MYSQL Console using the command code `sudo mysql`

<img width="620" alt="CONNECTED TO MySQL server by loggin in to the console" src="https://user-images.githubusercontent.com/115954100/208170557-8e6a4fe2-26e1-4dc5-9537-d96380e82915.PNG">

- I set a password for the root user using the command code `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';` with 'Password.1' as my default password.

<img width="677" alt="Running MySQL security script" src="https://user-images.githubusercontent.com/115954100/208170770-d527a094-3216-4f7f-8bdb-283e35d9317b.PNG">

- Using the command code `exit`, I exited the mysql shell

- I ran the interective script using the command code `sudo mysql_secure_installation`. This command enables me to configure and validate a new password plugin for mysql root user.

<img width="784" alt="Interactive script and new password validation" src="https://user-images.githubusercontent.com/115954100/208171491-148fe3a7-2927-4421-9e56-39e32028239c.PNG">

- After I enabled and validated a new password, I changed the root password, removed some anonymous users and the test database, disabled remote root logins and I loaded the new rule so that mysql save the changes.

- Finally I ran a command code to check if I can log in to MYSQL Console with the new password using the command code `sudo mysql -p`.

<img width="602" alt="loggin in with my new password" src="https://user-images.githubusercontent.com/115954100/208172975-b79198ee-f71c-4efa-84e0-40a86669bfa0.PNG">


***STEP 3: INSTALLING PHP***

- In this step, I need a component in my setup that will process code to display dynamic content to the end user. PHP serves this function.

- A PHP module that will allow PHP communicate with *mysql-based databases*, so *php-mysql* is needed.

- And for my Apache to handle PHP files, *libapache2-mod-php* is also needed.

- So with a single command code `sudo apt install php libapache2-mod-php php-mysql` I installed *PHP, PHP-MYSQL and LIBAPACHE2-MOD-PHP*.

<img width="900" alt="PHP_PHP-MySQL_LIBAPACHE2-MOD-PHP 3 IN 1 Installation" src="https://user-images.githubusercontent.com/115954100/208173920-40e19cf3-bc0b-4e95-8109-b8171a539a38.PNG">

- After the installation process of the previous step, I confirmed the PHP version using the command code `php -v`

<img width="483" alt="Confirming PHP version" src="https://user-images.githubusercontent.com/115954100/208174113-fe0a932f-3439-4467-a041-78962698b866.PNG">

- My LAMP is now installed and fully operational.


***STEP 4: CREATING A VIRTUAL HOST FOR MY WEBSITE USING APACHE***

- In this step, a doamin is created called PROJECTLAMP. From the configured server block enabled on Ubuntu, I created a directory for my *PROJECTLAMP* using the command code `sudo mkdir /var/www/projectlamp`.

- I assigned ownership of the created directory with my current system user using the command code `sudo chown -R $USER:$USER /var/www/projectlamp`.

- With a preferred command line edition, I created and opened a new configuration file in *Apache's sites-available directory* using the command code `sudo vi /etc/apache2/sites-available/projectlamp.conf`.

- This created a blank file. I pasted some bare-bone configuration, then I entered *I* on the keyboard to gain access to the insert mode. I saved and closed this configuration file by typing the *esc button, :, wq*, then I hit the *enter key* to save the file.

<img width="774" alt="Creating a blank file and insert mode" src="https://user-images.githubusercontent.com/115954100/208175127-127590f5-c759-41d3-8f9c-2bbf2b8c662c.PNG">

- I used the command code `sudo ls /etc/apache2/sites-available` to show the new file in the sites- available directory

<img width="586" alt="New file in site available directory" src="https://user-images.githubusercontent.com/115954100/208175245-0750087f-e6d6-4747-862e-b988e4ed2750.PNG">

- With the new VirtualHost configuration, Apache is now serving *Projectlamp* using /var/www/projectlampl as it's web directory. Thereafter, this new *VirtualHost* was enabled using the command code `sudo a2ensite projectlamp`.

<img width="440" alt="Enabling new virtual host" src="https://user-images.githubusercontent.com/115954100/208175350-6466b472-52b9-4ef1-b54f-df53b4eb4d7c.PNG">

- In order for Apache default configuration not to overwrite my *VirtualHost*, I disabled the default website that comes installed with Apache using the command code `sudo a2dissite 000-default`.

<img width="419" alt="Disenabling Apache default website" src="https://user-images.githubusercontent.com/115954100/208175434-e55738af-9f84-4389-9ff8-6d56f3cdab28.PNG">

- So I tested for syntax error to make sure my configuation file doesn't contain syntax error using the command code `sudo apache2ctl configtest`.

<img width="433" alt="No syntax error in my configuration" src="https://user-images.githubusercontent.com/115954100/208175739-486e9f18-68f2-4061-bd38-2878429cfb73.PNG">

- Finally, I reloaded the Apache for the new changes to take effect using the command code `sudo systemctl reload apache2`.

- With my new website active but with an empty web root */var/www/projectlamp*, I created an *index.html* file in that location just to test that the virtual host works as expected using the command code `sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`.

- Using my public ip, I opened my website url typing `http://<Public-IP-Address>:80`. As expected, Apache worked.

<img width="800" alt="accessing my public ip on the web" src="https://user-images.githubusercontent.com/115954100/208176116-f9d89f82-8470-4fc9-a617-082718eedd0e.PNG">


***STEP 5: ENABLE PHP ON A WEBSITE***

- My default DirectoryIndex settings is now on apache. In PHP application, a file named *'index.html'* will always take priority over an *'index.php'* file because this is useful in setting up maintenance page in PHP.

- To change this pattern, I edited the *'/etc/apache2/mods-enabled/dir.conf'* file and change the order in which the *'index.php'* file is listed within the *DirectoryIndex directive* by using the command code `sudo vim /etc/apache2/mods-enabled/dir.conf` then follow by the command code,
```
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```

- I gained access to the insert mode tping *'I'* and hitting the enter button.

- I saved the priority order using the *Esc* key, *wq* and then hit the enter button.

- Then I reloaded Apache so the changes take effect using the command code `sudo systemctl reload apache2`.


<img width="507" alt="PHP VALID CODE ADDED" src="https://user-images.githubusercontent.com/115954100/208185336-f4869179-5fd9-41c9-86bc-71e47186e76b.PNG">

- Now that my website files and folders can be hosted on a custom location, I finally created a PHP script to test that PHP is properly installed and configured on the server and also to test if Apache is able to handle and process request for PHP files.

- Inside my custom root folder, I created a new file named *'index.php'* using the command code `vim /var/www/projectlamp/index.php`.

- This opened a blank file showing a valid PHP code

```
<?php
phpinfo();
```

- After this, I saved the file and refreshed my url page.

<img width="796" alt="PHP installation working perfectly" src="https://user-images.githubusercontent.com/115954100/208186092-17e7b21e-33fd-4073-a663-911c093d29ea.PNG">

<img width="550" alt="After refreshing the page" src="https://user-images.githubusercontent.com/115954100/208186197-f19a8cd9-a669-4ba7-afa1-60b54708283b.PNG">

- Due to the sensitive information contained in the PHP environment, I deleted the file created using the command code `sudo rm /var/www/projectlamp/index.php`.
