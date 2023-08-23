# Add more ports to apache2 (also 1 more website) to create Cloudflare CNAME subdomain via port.
- Become sudo by doing the following command:
```
sudo su
```
- cd into "/etc/apache2/sites-available/"
```
cd /etc/apache2/sites-available/
```
- edit the handler config file:
```
nano sitename-handler.conf
```
- in the file put:
```
<VirtualHost *:80>
    ServerName THE_URL_WITH_THE_SUBDOMAIN
    DocumentRoot PATH_FOR_THE_WEBSITE_FILES

    ProxyPass / http://127.0.0.1:YOUR_PORT/
    ProxyPassReverse / http://127.0.0.1:YOUR_PORT/

    <Directory PATH_FOR_THE_WEBSITE_FILES>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```
- change "YOUR_PORT" to the desire port, the THE_URL_WITH_THE_SUBDOMAIN to your domain with the subdomain and change PATH_FOR_THE_WEBSITE_FILES for the path of your website's files.
- now press the following keys to save and exit:
```
  CTRL + O, ENTER, CTRL + X
```
- now, edit the 2nd conf file by follows:
```
sudo nano /etc/apache2/sites-available/YOUR_WEBSITE_NAME.conf
```
- replace the YOUR_WEBSITE_NAME with your actual website name
- write the following into the text editor:
```
<VirtualHost *:WANTED_PORT>
    ServerAdmin example@mail.com
    ServerName THE_URL_WITH_THE_SUBDOMAIN
    DocumentRoot PATH_FOR_THE_WEBSITE_FILES

    ErrorLog ${APACHE_LOG_DIR}/WEBSITE-NAME_error.log
    CustomLog ${APACHE_LOG_DIR}/WEBSITE-NAME_access.log combined

    <Directory PATH_FOR_THE_WEBSITE_FILES>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```
- replcae PATH_FOR_THE_WEBSITE_FILES with the path of your website's files, WEBSITE-NAME with the name of your website the WANTED_PORT for the port you want the system to use and lastly the "example@mail.com" with the managers mail.
- now, enable the configs file via the following command:
```
sudo a2enconf YOUR_WEBSITE_NAME.conf
sudo a2enconf sitename-handler.conf
sudo service apache2 reload
sudo service apache2 restart
```
make sure to switch sitename-handle and YOUR_WEBSITE_NAME with the names of you config files.

## now, last 2 things:
- nano ports.conf file and add your port:
```
sudo nano /etc/apache2/ports.conf
```
and add the following line:

```
Listen YOUR_PORT
```
replace YOUR_PORT with your new website's port 

## One Last Thing!

run the following commands to reload and restart the apache2 server to apply channges:
```
sudo service apache2 reload
sudo service apache2 restart
```
