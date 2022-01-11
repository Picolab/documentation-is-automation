Strange:

```
ubuntu@ip-172-18-10-145:~$ sudo certbot renew
Saving debug log to /var/log/letsencrypt/letsencrypt.log

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/manifold.picolabs.io.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Cert not yet due for renewal

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

The following certs are not due for renewal yet:
  /etc/letsencrypt/live/manifold.picolabs.io/fullchain.pem expires on 2021-11-08 (skipped)
No renewals were attempted.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
ubuntu@ip-172-18-10-145:~$ sudo certbot certonly --force-renew -d manifold.picolabs.io
Saving debug log to /var/log/letsencrypt/letsencrypt.log

How would you like to authenticate with the ACME CA?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: Nginx Web Server plugin (nginx)
2: Spin up a temporary webserver (standalone)
3: Place files in webroot directory (webroot)
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-3] then [enter] (press 'c' to cancel): 1
Plugins selected: Authenticator nginx, Installer None
Starting new HTTPS connection (1): acme-v02.api.letsencrypt.org
Renewing an existing certificate

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/manifold.picolabs.io/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/manifold.picolabs.io/privkey.pem
   Your cert will expire on 2021-11-12. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot
   again. To non-interactively renew *all* of your certificates, run
   "certbot renew"
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le

ubuntu@ip-172-18-10-145:~$ 
```

Yet a browser shows "Expires: Sunday, August 15, 2021 at 1:12:20 PM Mountain Daylight Time"

## added Monday, August 16, 2021 at 9:41 AM

Went to the website and it did not display anything, and showed an expired certificate.

Logged in and ran the same two commands (above) with similar results.

Went to the website and it displayed normally, but still showed an expired certificate.

Held down shift key and reloaded the page and it displayed normally and shows a certificate valid until 
Friday, November 12, 2021 at 7:00:49 AM Mountain Standard Time.

## added Tuesday, November 16, 2021 at 8:42 AM

Certificate now valid until Thursday, January 13, 2022 at 8:30:53 AM Mountain

## added Tuesday, January 11, 2022

Certificate now valid until Monday, February 14, 2022 at 7:39:39 AM Mountain Standard Time
