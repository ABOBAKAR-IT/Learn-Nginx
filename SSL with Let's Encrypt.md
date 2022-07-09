# Step 1 — Installing Certbot
```
sudo apt install certbot python3-certbot-nginx
```
# Step 2 — Obtaining an SSL Certificate
Certbot provides a variety of ways to obtain SSL certificates through plugins. The Nginx plugin will take care of reconfiguring Nginx and reloading the config whenever necessary. To use this plugin, type the following:
```
sudo certbot --nginx -d abobakar.me -d www.abobakar.me
```
This runs `certbot` with the `--nginx` plugin, using `-d` to specify the domain names we’d like the certificate to be valid for.\
If this is your first time running `certbot`, you will be prompted to enter an email address and agree to the terms of service. After doing so, certbot will communicate with the `Let’s Encrypt` server, then run a challenge to verify that you control the domain you’re requesting a certificate for.\
If that’s successful, `certbot` will ask how you’d like to configure your `HTTPS` settings.
```
Output
Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: No redirect - Make no further changes to the webserver configuration.
2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
new sites, or if you're confident your site works on HTTPS. You can undo this
change by editing your web server's configuration.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel):
```
Select your choice then hit `ENTER`. The configuration will be updated, and Nginx will reload to pick up the new settings.\
If you test your server using the <a href="https://www.ssllabs.com/ssltest/" tra>SSL Labs Server Test</a>, it will get an `A` grade.

# Step 3 — Verifying Certbot Auto-Renewal
Let’s Encrypt’s certificates are only valid for ninety days. This is to encourage users to automate their certificate renewal process. The `certbot` package we installed takes care of this for us by adding a systemd timer that will run twice a day and automatically renew any certificate that’s within thirty days of expiration.\
You can query the status of the timer with `systemctl`:
```
sudo systemctl status certbot.timer
```
```
Output
● certbot.timer - Run certbot twice daily
     Loaded: loaded (/lib/systemd/system/certbot.timer; enabled; vendor preset: enabled)
     Active: active (waiting) since Mon 2020-05-04 20:04:36 UTC; 2 weeks 1 days ago
    Trigger: Thu 2020-05-21 05:22:32 UTC; 9h left
   Triggers: ● certbot.service
   ```
   To test the `renewal process`, you can do a dry run with `certbot`:
   ```
   sudo certbot renew --dry-run
   ```
   If you see no errors, you’re all set. When necessary, Certbot will renew your certificates and reload Nginx to pick up the changes. If the automated renewal process ever fails, Let’s Encrypt will send a message to the email you specified, warning you when your certificate is about to expire.
