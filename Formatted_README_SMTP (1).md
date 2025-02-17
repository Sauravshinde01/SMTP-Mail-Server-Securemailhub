# SMTP Mail Server Setup

**Setting up an iRedMail server for a custom domain**

**Prerequisites:**

A Contabo VPS.

A domain name that you want to use for your email server.

**Contabo:**

Set up a Virtual Private Server (VPS) with Ubuntu to run iRedMail.

![image](https://github.com/user-attachments/assets/7890c207-eeb4-4a4b-a44e-18289f4efd92)


**Set up reverse DNS:**

This will allow us to access your VPS public IP with the domain name. To do this, we must update the reverse DNS records for the VPS as below.

![image](https://github.com/user-attachments/assets/8d41cf49-acd0-46f5-9c00-85dabdc31de5)


**Connect to the VPS using SSH:**

We can use PowerShell to connect to the VPS. To do this, open PowerShell and run the following command: ssh root@31.220.95.22 (Contabo public IP)

![image](https://github.com/user-attachments/assets/88c4c205-3e67-49f5-9ccf-1d8d212966ad)


**Change the hostname of the VPS:**

To do this, run the following command: hostnamectl set-hostname mail.securemailhub.me
![image](https://github.com/user-attachments/assets/1aee390b-8f41-44d2-8e73-174bcd8b9719)



**Update the /etc/hosts file:**

To do this, open the /etc/hosts file in a text editor and add the following line:

![image](https://github.com/user-attachments/assets/0ae6771c-f1a0-4266-992d-63fbb1082dd2)




Next, I updated the Ubuntu packages and installed gzip using the following command:

**sudo apt update && sudo apt upgrade -y**

**apt install gzip**

![image](https://github.com/user-attachments/assets/a4aaea5f-f854-4b8a-b804-b0b9bad11db2)

![image](https://github.com/user-attachments/assets/aa32e1cf-c4d5-4ec1-9846-00e0c26f03a8)



I then downloaded the latest version of iRedMail using:

**wget https://github.com/iredmail/iRedMail/archive/refs/tags/1.6.6.tar.gz**  


![image](https://github.com/user-attachments/assets/405723c7-2835-4a8a-92fd-586f53d84959)



I extracted the tar file using tar zxvf 1.6.6.tar.gz.

![image](https://github.com/user-attachments/assets/21d16fd1-fa8b-43af-a72c-bad48325c5c6)


I then installed iRedMail using command: bash iRedMail.sh

![image](https://github.com/user-attachments/assets/c6862be3-0aad-499a-a606-93589bcea6b4)






I opted for NGINX for the web server and MariaDB for the database.




![image](https://github.com/user-attachments/assets/df580b6b-9058-4313-a055-784987cc7ddd)

![image](https://github.com/user-attachments/assets/001f43de-dba7-40cd-9903-4ac27e008b23)

![image](https://github.com/user-attachments/assets/c7ef565e-4471-40ab-a402-98ee8d246902)




I provided my first mail domain name as securemailhub.me.

![image](https://github.com/user-attachments/assets/e4ba6f7f-5f99-4ded-928f-e477169034f2)

![image](https://github.com/user-attachments/assets/00abaeeb-91af-45de-869c-64cbf8f1616d)

![image](https://github.com/user-attachments/assets/3a862220-9aff-4adf-97b6-559ffc291377)
 
![image](https://github.com/user-attachments/assets/0e4487bc-9ade-47e2-b868-bc9cbd0cfcb1)



After the installation was complete, I got the DKIM records using the following command: 

**amavisd-new showkeys**


![image](https://github.com/user-attachments/assets/a2e5146a-5413-4383-b76a-0216c71fd9cd)




I then installed SSL by installing two essential packages on my system, certbot and python3-certbot-nginx, using the following command:

**apt install certbot python3-certbot-nginx -y**

![image](https://github.com/user-attachments/assets/aa83a8b0-0293-47ad-ba92-91d6bb8df17e)


To generate the SSL certificate, I utilized Certbot using the following command:

**certbot certonly --webroot -d mail.securemailhub.me -w /var/www/html**

![image](https://github.com/user-attachments/assets/cbcf1da4-76a1-4605-921d-9cdee95d865e)


After obtaining the SSL certificate, we must configure my server applications to use it. Certbot stores my SSL certificate files in a specific directory, which is /etc/letsencrypt/live/ on my Linux system.

To configure my server applications to use the SSL certificate, I typically point them to the fullchain.pem and privkey.pem files.



![image](https://github.com/user-attachments/assets/f4556099-ebb8-46b4-8e31-a57f809831e7)

![image](https://github.com/user-attachments/assets/f38e2237-b995-4794-b8c6-908e11a60a5e)

![image](https://github.com/user-attachments/assets/bf64d641-f96b-4e27-ae47-5eb3394cf545)




Finally, I restarted iRedMail, Nginx, postfix, and dovecot and rebooted the VPS machine.


![image](https://github.com/user-attachments/assets/7a2cb98f-7014-4f6b-9feb-4b37b946850f)




**Setting up DNS records at domain:**

Updated Dmarc, DKIM and SPF records as below.

![image](https://github.com/user-attachments/assets/dc3c0c0b-658c-4f46-b7f1-805978285f5f)

![image](https://github.com/user-attachments/assets/dd7bd95e-cd15-4316-8096-b0b4a6257a68)





We can access the admin panel from mail.securemailhub.me/iredadmin. Admin can add new users and manage the mail server settings.


![image](https://github.com/user-attachments/assets/d5cf5196-bbdf-4303-abe5-c2bb658db316)

![image](https://github.com/user-attachments/assets/c26d8a9b-81ef-4b0a-b773-aab47abea220)







Adding new user for the new custom domain.


![image](https://github.com/user-attachments/assets/0f0bedbe-6ed3-4099-9eb3-9c64f51a21bb)

![image](https://github.com/user-attachments/assets/c2182b5a-b913-4c00-9419-a879c4d80017)






We can access the mail client from mail.securemailhub.me/mail. User should log in with their account credentials to access mail records.



![image](https://github.com/user-attachments/assets/93cedd82-f5bb-48c0-8579-112aaca7b6f7)

![image](https://github.com/user-attachments/assets/88c604c1-36dc-4009-b0a7-1b0eab2f3153)




**Mail results:**

Mail sent to TA

![image](https://github.com/user-attachments/assets/d3a4b92c-d254-481d-8207-5fe1afecbb54)


Mail received from the TA.

![image](https://github.com/user-attachments/assets/052606e9-0f85-4af2-8ecd-86841218cd4e)


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
