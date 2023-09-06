From Blase's hw from security

### Install Apache as your web server (0 points, but required)

Great, now you're logged into your VM and seeing an Ubuntu command prompt. Now, you need to install a webserver (we'll use Apache) and a way to create databases (we'll use MySQL). On the command line of your VM, follow these steps, which are based on [https://phoenixnap.com/kb/how-to-install-lamp-stack-on-ubuntu](https://phoenixnap.com/kb/how-to-install-lamp-stack-on-ubuntu), yet adjusted for what we'll need.

+ *sudo apt-get update*
+ *sudo apt-get install apache2*
+ *sudo rm /etc/apache2/sites-available/default-ssl.conf* (to remove a file we don't need)
+ *sudo vi /etc/apache2/sites-available/000-default.conf*
+ This brings you into a config file, where you'll notice the following line commented out: *#ServerName www.example.com*. Uncomment this line and change it to match your subdomain (e.g., *ServerName student.example.com*)
+ *sudo service apache2 restart* (to restart Apache)
+ Verify that this worked by opening up a browser on your own computer and going to your server (e.g., *http://student.example.com*, noting the http (not https). You should see the Apache2 Ubuntu Default Page.

### Get a certificate (1 point)

Ok. Now let's get an HTTPS certificate for your server using Let's Encrypt. Run the following:

+ *sudo apt install python3-certbot-apache*
+ *sudo letsencrypt*
+ When you are asked about redirecting to HTTPS, choose "Redirect," which is choice 2.
+ *sudo service apache2 restart* (to restart Apache)
+ Verify that this worked by opening up a browser on your own computer and going to your server (e.g., *https://student.example.com*, noting the s in https). You should still see the Apache2 Ubuntu Default Page, but now you're connected over TLS.


### Permissions

https://www.internalpointers.com/post/right-folder-permission-website

sudo chown -R [username] /var/www/
sudo addgroup [group_name]

sudo usermod -a -G [groupName] <userName>

chgrp -R [group_name] /var/www/

chmod -R 755 /var/www/


### Database
https://www.postgresqltutorial.com/postgresql-getting-started/install-postgresql-linux/
https://medium.com/coding-blocks/creating-user-database-and-adding-access-on-postgresql-8bfcd2f4a91e


sudo -u postgres psql



psql <- start
\q stop

\c [database] <- pick database



SELECT count(*) FROM new_reddit;
SELECT * FROM reddit LIMIT 1;


#DELETE * FROM reddit;
DROP TABLE tblname;

\dt <- list tables

sudo -u postgres psql

CREATE USER [user] WITH ENCRYPTED PASSWORD '[password]';
GRANT INSERT, UPDATE ON [table] TO [user];

GRANT SELECT ON [table] TO [user];

