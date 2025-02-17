# SMTP Mail Server Setup

Setting up an iRedMail server for a custom domain

Prerequisites:

A Contabo VPS.

A domain name that you want to use for your email server.

Contabo:

Set up a Virtual Private Server (VPS) with Ubuntu to run iRedMail.



Set up reverse DNS:

This will allow us to access your VPS public IP with the domain name. To do this, we must update the reverse DNS records for the VPS as below.



Connect to the VPS using SSH:

We can use PowerShell to connect to the VPS. To do this, open PowerShell and run the following command: ssh root@31.220.95.22 (Contabo public IP)



Change the hostname of the VPS:

To do this, run the following command: hostnamectl set-hostname mail.securemailhub.me



Update the /etc/hosts file:

To do this, open the /etc/hosts file in a text editor and add the following line:





Next, I updated the Ubuntu packages and installed gzip using the following command:

sudo apt update && sudo apt upgrade -y

apt install gzip






I then downloaded the latest version of iRedMail using:

wget  







I extracted the tar file using tar zxvf 1.6.6.tar.gz.



I then installed iRedMail using command: bash iRedMail.sh







I opted for NGINX for the web server and MariaDB for the database.







I provided my first mail domain name as securemailhub.me.



 



After the installation was complete, I got the DKIM records using the following command: 

amavisd-new showkeys





I then installed SSL by installing two essential packages on my system, certbot and python3-certbot-nginx, using the following command:

apt install certbot python3-certbot-nginx -y



To generate the SSL certificate, I utilized Certbot using the following command:

certbot certonly --webroot -d mail.securemailhub.me -w /var/www/html



After obtaining the SSL certificate, we must configure my server applications to use it. Certbot stores my SSL certificate files in a specific directory, which is /etc/letsencrypt/live/ on my Linux system.

To configure my server applications to use the SSL certificate, I typically point them to the fullchain.pem and privkey.pem files.







Finally, I restarted iRedMail, Nginx, postfix, and dovecot and rebooted the VPS machine.






Setting up DNS records at domain:

Updated Dmarc, DKIM and SPF records as below.






We can access the admin panel from mail.securemailhub.me/iredadmin. Admin can add new users and manage the mail server settings.









Adding new user for the new custom domain.









We can access the mail client from mail.securemailhub.me/mail. User should log in with their account credentials to access mail records.








Mail results:

Mail sent to TA



Mail received from the TA.



a. A domain name is required to create an SMTP mail server because it serves as the unique identifier for your email server. It is used to route emails to the correct server and to authenticate the server when sending emails. 



b. MX, SPF, and DKIM records are used to ensure email security. 

MX records specify the mail server responsible for accepting incoming emails for your domain. 

SPF records are used to verify that the email was sent from an authorized server. 

DKIM records are used to verify that the email was not tampered with during transmission. 



c. DNS propagation is the time it takes for DNS changes to take effect across the internet. It can take up to 48 hours for DNS changes to propagate fully. You must wait for DNS propagation after making DNS changes to ensure your email server is accessible to everyone.



a. SSH is used to connect to the Virtual Private Server (VPS) for installing iRedMail because it provides a secure way to access the server remotely. 


b. OpenLDAP is a backend for storing mail accounts that provides a centralized database for storing user information. It is used to manage user accounts and passwords and to authenticate users when they login to their email accounts. 



c. Roundcube and SOGo are both webmail options that provide a web-based interface for accessing email. 

Roundcube is a simple and lightweight webmail client that is easy to use and has a clean interface.

 SOGo is a more advanced webmail client with features like calendar and contact management. 

You can choose Roundcube for a simple and easy-to-use webmail client, and SOGo if you need more advanced features. 



d. Reviewing the installation choices before proceeding is essential because it ensures that the installation is configured correctly and all necessary components are installed.



a. Configuring the mail client is necessary after setting up the SMTP mail server because it allows you to send and receive emails using your email account. The configuration will help to connect to the server, authentication and to mange the mail incoming and outgoing mails overall.



b. To configure the mail client to work with the iRedMail server, you would need to enter the following information:

We should configure the iRedMail server address, which will be used to send email messages. The default SMTP server address is `mail.securemailhub.me:587`.

The username for your email account on the iRedMail server.

The password for your email account on the iRedMail server.

We should configure the security settings. The iRedMail server supports SSL/TLS encryption for IMAP, POP3, and SMTP connections. It is recommended that you enable SSL/TLS encryption in your mail client to protect your email messages.

Configuring port numbers if required. The iRedMail server uses the following default port numbers: 

IMAP: 993

POP3: 995

SMTP: 587

If you are using a non-standard port number for any of these services, you will need to configure the corresponding port number in your mail client. 



## Screenshots
![Screenshot 1](screenshot_1.png)

![Screenshot 2](screenshot_2.png)

![Screenshot 3](screenshot_3.png)

![Screenshot 4](screenshot_4.png)

![Screenshot 5](screenshot_5.png)

![Screenshot 6](screenshot_6.png)

![Screenshot 7](screenshot_7.png)

![Screenshot 8](screenshot_8.png)

![Screenshot 9](screenshot_9.png)

![Screenshot 10](screenshot_10.png)

![Screenshot 11](screenshot_11.png)

![Screenshot 12](screenshot_12.png)

![Screenshot 13](screenshot_13.png)

![Screenshot 14](screenshot_14.png)

![Screenshot 15](screenshot_15.png)

![Screenshot 16](screenshot_16.png)

![Screenshot 17](screenshot_17.png)

![Screenshot 18](screenshot_18.png)

![Screenshot 19](screenshot_19.png)

![Screenshot 20](screenshot_20.png)

![Screenshot 21](screenshot_21.png)

![Screenshot 22](screenshot_22.png)

![Screenshot 23](screenshot_23.png)

![Screenshot 24](screenshot_24.png)

![Screenshot 25](screenshot_25.png)

![Screenshot 26](screenshot_26.png)

![Screenshot 27](screenshot_27.png)

![Screenshot 28](screenshot_28.png)

![Screenshot 29](screenshot_29.png)

![Screenshot 30](screenshot_30.png)

![Screenshot 31](screenshot_31.png)

![Screenshot 32](screenshot_32.png)

![Screenshot 33](screenshot_33.png)

![Screenshot 34](screenshot_34.png)

