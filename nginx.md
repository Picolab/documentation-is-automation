# Using `nginx`

## Installation
I followed the instructions for ubuntu in [this page](http://nginx.org/en/linux_packages.html)

The last step seems to be stuck at 
```
Processing triggers for systemd (245.4-4ubuntu3.11) ...
```

Waiting... while looking up this message, the process finished, so I am assuming `nginx` is now installed.

## Getting started
Following instructions on [this page](http://nginx.org/en/docs/beginners_guide.html)

### Preparation

Per the instructions, created a couple of directories:
```
$ sudo mkdir -p /data/www
$ sudo mkdir -p /data/images
```

Located the `nginx.conf` file in `/etc/nginx/` and note that it sets up a number of things and ends by 
```
    include /etc/nginx/conf.d/*.conf;
```
which contains only `default.conf`. After starting `nginx`
```
$ sudo nginx
```
its default page shows, whereas before I began, nothing showed when visiting the server (an EC2 instance) on port 80.

The instructions suggest commenting out existing things in the `default.conf` file, so before doing that, I made a copy:
```
$ sudo cp default.conf default.conf-original
```
Now, editing the `default.conf` file, I removed most of the commented out lines, and began following the instructions.
With one difference, which is that they suggest using an `http` directive, but that is contained in the `nginx.conf` file which will
include mine, so I omit that wrapper.

Added these `location`s:
```
    location / {
        root   /data/www;
        index  index.html index.htm;
    }

    location /images/ {
        root   /data;
    }
```
Also, put a simple `index.html` file in `/data/www/` and a simple image in `/data/images/` and had `nginx` reload the configuration:
```
$sudo nginx -s reload
```
And it works!

