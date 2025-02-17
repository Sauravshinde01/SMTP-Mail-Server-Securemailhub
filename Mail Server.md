**Setting up an iRedMail server for a custom domain**

**Prerequisites:**

- A Contabo VPS.

- A domain name that you want to use for your email server.

**Contabo:**

Set up a Virtual Private Server (VPS) with Ubuntu to run iRedMail.

![A screenshot of a computer Description automatically
generated](media/image1.png){width="5.147037401574803in"
height="3.029381014873141in"}

**Set up reverse DNS:**

This will allow us to access your VPS public IP with the domain name. To
do this, we must update the reverse DNS records for the VPS as below.

![A screenshot of a computer Description automatically
generated](media/image2.png){width="5.459617235345582in"
height="3.2133562992125984in"}

**Connect to the VPS using SSH:**

We can use PowerShell to connect to the VPS. To do this, open PowerShell
and run the following command: **ssh root@31.220.95.22** (Contabo public
IP)

![](media/image3.png){width="6.5in" height="3.692962598425197in"}

**Change the hostname of the VPS:**

To do this, run the following command: **hostnamectl set-hostname
mail.securemailhub.me**

![](media/image4.png){width="6.5in" height="3.692962598425197in"}

**Update the /etc/hosts file:**

To do this, open the /etc/hosts file in a text editor and add the
following line:

![](media/image5.png){width="6.5in" height="3.692962598425197in"}

Next, I updated the Ubuntu packages and installed gzip using the
following command:

**sudo apt update && sudo apt upgrade -y**

**apt install gzip**

![A screenshot of a computer program Description automatically
generated](media/image6.png){width="5.837550306211724in"
height="3.3166765091863515in"}

![](media/image7.png){width="6.5in" height="3.692962598425197in"}

I then downloaded the latest version of iRedMail using:

wget
<https://github.com/iredmail/iRedMail/archive/refs/tags/1.6.6.tar.gz>

![A screenshot of a computer program Description automatically
generated](media/image8.png){width="6.5in"
height="3.6979166666666665in"}

I extracted the tar file using tar zxvf 1.6.6.tar.gz.

![A screenshot of a computer program Description automatically
generated](media/image9.png){width="6.5in"
height="3.6979166666666665in"}

I then installed iRedMail using command: bash iRedMail.sh

![A screenshot of a computer screen Description automatically
generated](media/image10.png){width="6.5in"
height="3.6930555555555555in"}

I opted for NGINX for the web server and MariaDB for the database.

![A computer screen with a message Description automatically
generated](media/image11.png){width="6.5in"
height="3.6930555555555555in"}

![A computer screen shot of a computer Description automatically
generated](media/image12.png){width="6.5in"
height="3.6930555555555555in"}

![A computer screen with a message Description automatically
generated](media/image13.png){width="6.5in"
height="3.6930555555555555in"}

I provided my first mail domain name as securemailhub.me.

![A computer screen shot of a message Description automatically
generated](media/image14.png){width="6.5in"
height="3.6930555555555555in"}

![A screenshot of a computer Description automatically
generated](media/image15.png){width="6.5in"
height="2.8694444444444445in"}![A computer screen with a blue and black
screen Description automatically
generated](media/image16.png){width="6.5in"
height="3.6930555555555555in"} ![A screenshot of a computer Description
automatically generated](media/image17.png){width="6.5in"
height="3.6930555555555555in"}

After the installation was complete, I got the DKIM records using the
following command:

**amavisd-new showkeys**

![](media/image18.png){width="6.5in" height="3.692962598425197in"}

I then installed SSL by installing two essential packages on my system,
certbot and python3-certbot-nginx, using the following command:

**apt install certbot python3-certbot-nginx -y**

![A screenshot of a computer program Description automatically
generated](media/image19.png){width="6.5in"
height="3.6930555555555555in"}

To generate the SSL certificate, I utilized Certbot using the following
command:

**certbot certonly \--webroot -d mail.securemailhub.me -w
/var/www/html**

![](media/image20.png){width="6.5in" height="3.692962598425197in"}

After obtaining the SSL certificate, we must configure my server
applications to use it. Certbot stores my SSL certificate files in a
specific directory, which is /etc/letsencrypt/live/ on my Linux system.

To configure my server applications to use the SSL certificate, I
typically point them to the fullchain.pem and privkey.pem files.

![](media/image21.png){width="6.5in" height="3.692962598425197in"}

![A screenshot of a computer Description automatically
generated](media/image22.png){width="6.5in"
height="3.6930555555555555in"}

![A screenshot of a computer Description automatically
generated](media/image23.png){width="6.5in"
height="3.6930555555555555in"}

Finally, I restarted iRedMail, Nginx, postfix, and dovecot and rebooted
the VPS machine.

![A screen shot of a computer Description automatically
generated](media/image24.png){width="6.5in"
height="3.6930555555555555in"}

**Setting up DNS records at domain:**

Updated Dmarc, DKIM and SPF records as below.

![](media/image25.png){width="6.5in" height="3.8255205599300086in"}

![A screenshot of a computer Description automatically
generated](media/image26.png){width="6.5in"
height="3.8256944444444443in"}**  
**

We can access the admin panel from **mail.securemailhub.me/iredadmin**.
Admin can add new users and manage the mail server settings.

![A screenshot of a computer Description automatically
generated](media/image27.png){width="6.5in"
height="3.8256944444444443in"}

![A screenshot of a computer Description automatically
generated](media/image28.png){width="6.5in"
height="3.8256944444444443in"}

Adding new user for the new custom domain.

![A screenshot of a computer Description automatically
generated](media/image29.png){width="6.5in"
height="3.8256944444444443in"}

![A screenshot of a computer Description automatically
generated](media/image30.png){width="6.5in"
height="3.8256944444444443in"}

We can access the mail client from **mail.securemailhub.me/mail**. User
should log in with their account credentials to access mail records.

![A screenshot of a computer Description automatically
generated](media/image31.png){width="6.5in"
height="3.8256944444444443in"}

![A screenshot of a computer Description automatically
generated](media/image32.png){width="6.5in"
height="3.8256944444444443in"}

**  
**

**Mail results:**

Mail sent to TA

![](media/image33.png){width="6.5in" height="3.8255205599300086in"}

Mail received from the TA.

![A screenshot of a computer Description automatically
generated](media/image34.png){width="6.5in"
height="3.8256944444444443in"}

1.  a\. A domain name is required to create an SMTP mail server because
    it serves as the unique identifier for your email server. It is used
    to route emails to the correct server and to authenticate the server
    when sending emails.

b\. MX, SPF, and DKIM records are used to ensure email security.

- MX records specify the mail server responsible for accepting incoming
  emails for your domain.

- SPF records are used to verify that the email was sent from an
  authorized server.

- DKIM records are used to verify that the email was not tampered with
  during transmission.

c\. DNS propagation is the time it takes for DNS changes to take effect
across the internet. It can take up to 48 hours for DNS changes to
propagate fully. You must wait for DNS propagation after making DNS
changes to ensure your email server is accessible to everyone.

2.  a\. SSH is used to connect to the Virtual Private Server (VPS) for
    installing iRedMail because it provides a secure way to access the
    server remotely.

b\. OpenLDAP is a backend for storing mail accounts that provides a
centralized database for storing user information. It is used to manage
user accounts and passwords and to authenticate users when they login to
their email accounts.

c\. Roundcube and SOGo are both webmail options that provide a web-based
interface for accessing email.

- Roundcube is a simple and lightweight webmail client that is easy to
  use and has a clean interface.

- SOGo is a more advanced webmail client with features like calendar and
  contact management.

- You can choose Roundcube for a simple and easy-to-use webmail client,
  and SOGo if you need more advanced features.

d\. Reviewing the installation choices before proceeding is essential
because it ensures that the installation is configured correctly and all
necessary components are installed.

3.  a\. Configuring the mail client is necessary after setting up the
    SMTP mail server because it allows you to send and receive emails
    using your email account. The configuration will help to connect to
    the server, authentication and to mange the mail incoming and
    outgoing mails overall.

b\. To configure the mail client to work with the iRedMail server, you
would need to enter the following information:

- We should configure the iRedMail server address, which will be used to
  send email messages. The default SMTP server address is
  \`mail.securemailhub.me:587\`.

- The username for your email account on the iRedMail server.

- The password for your email account on the iRedMail server.

- We should configure the security settings. The iRedMail server
  supports SSL/TLS encryption for IMAP, POP3, and SMTP connections. It
  is recommended that you enable SSL/TLS encryption in your mail client
  to protect your email messages.

- Configuring port numbers if required. The iRedMail server uses the
  following default port numbers:

  - IMAP: 993

  - POP3: 995

  - SMTP: 587

If you are using a non-standard port number for any of these services,
you will need to configure the corresponding port number in your mail
client.
