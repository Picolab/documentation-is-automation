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

## added Wednesday, April 6, 2022

Browser shows it will expire April 11, but `sudo certbot renew` won't renew saying it expires on 2022-05-18.
Forcing and `certbot` now says it "will expire 2022-07-05."
Browser now shows it valid until "Wednesday, May 18, 2022 at 7:34:10 AM Mountain".
I will never understand this.

## added Friday, July 8, 2022

Same kind of thing. `sudo certbot renew` won't renew, so had to force it again.
![Screen Shot 2022-07-08 at 15 14 25](https://user-images.githubusercontent.com/19273926/178071379-6f227417-3add-4db5-b81e-56b7b3f58a47.png)

## added Friday, August 12, 2022

Learned something new.
The certificate _has_ been renewed, and all that was needed was this command:
```
sudo service nginx restart
```
<img width="409" alt="Screen Shot 2022-08-12 at 09 23 10" src="https://user-images.githubusercontent.com/19273926/184387616-fae1d746-e670-4beb-8ab0-3bbbca43f88b.png">
I did a little investigating to see why that wasn't done after the auto-renewal of the certificate,
but didn't find anything.

## added Wednesday, October 5, 2022

Restarted `nginx`

<img width="450" alt="Screen Shot 2022-10-05 at 07 20 24" src="https://user-images.githubusercontent.com/19273926/194070656-043fb906-074a-4387-b7b9-3d231739105d.png">
