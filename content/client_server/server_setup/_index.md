+++
title = "Server Setup"
weight = 1
alwaysopen = true
+++

This is the guide for deploying the Eldiron server.

All shell commands listed below assume that you're using a root account.

## Prerequisites

### Host

You need a host for your Eldiron server to run on.

We recommend using cloud droplets with Ubuntu provided by [DigitalOcean](https://www.digitalocean.com/) as we're using them as well. The following instructions are tested on Ubuntu, and you will find that we give Ubuntu users a more detailed guide. But anyway, you have the right to choose your own.

### Rust

Eldiron is written in Rust, so you need Rust to compile Eldiron before deploying your own server from source code.

To install Rust, follow the [official instructions](https://www.rust-lang.org/learn/get-started).

_TLDR_:

- Unix-like OS (MacOS / Linux):

  ```bash
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
  ```

- Windows

  Download and run [`rustup-init.exe`](https://static.rust-lang.org/rustup/dist/i686-pc-windows-gnu/rustup-init.exe).

### Git

Git is essential when your source code is from a remote repository.

Visit the [official website for Git](https://git-scm.com/) if you don't have one installed on your machine.

### Other dependencies

Please read the [build local](../../basics/installation/_index.md#building-eldiron-locally) section carefully before building Eldiron. You might need some extra dependencies to be installed on your machine.

A cheatsheet for Ubuntu users:

```bash
apt update
apt install libasound2-dev
apt install pkg-config
pkg-config --libs --cflags alsa
```

## Build the server

Once you have the source code ready, whatever it's from the official Eldiron repository or your own forks, it's time to build the server.

Change your working directory to the root folder of the source. The building process is simple:

```bash
cargo build --release -p server
```

Hooray! You get an executable named `server` under `your-source-root/target/release` now.

There are various ways to deploy this server executable depends on the system you choose. For systems with `systemd` support, we recommend writing a systemd service for your server process.

### Eldiron-Cli

We provide a command line tool named [`eldiron-cli`](https://github.com/fralonra/eldiron-cli) which helps you with the above steps if you're not familiar working with shell. This cli tool provides an interactive interface to build your server from scratch, and deploy your server using systemd if it is available on your system.

Install `eldiron-cli`:

```bash
cargo install eldiron-cli
```

Build your server. It will automatically setup a systemd service if it is available:

```bash
eldiron server setup
```

Start the systemd server:

```bash
eldiron server start
```

Restart the systemd server:

```bash
eldiron server restart
```

Stop the systemd server:

```bash
eldiron server stop
```

### Client side

Once you have your server running, you have to make sure that your client application connects to the right url. Edit your client-side code and rebuild your client and you're done.

## Security

We recommend establishing a secure connection to protect your users.

Here's a guide to how to use [Let's Encrypt](https://letsencrypt.org/) and [Nginx](https://www.nginx.org/) to setup a HTTPS connection.

### Step 1. Install Nginx

Nginx is a free and open source web server, and used in production-level applications worldwide.

Install Nginx from your package manager or download it from the [official website](https://nginx.org/en/download.html).

DigitalOcean users can simply refer to the [official guide](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04) provided by DigitalOcean.

A cheatsheet for Ubuntu users:

```bash
apt update
apt install nginx
```

### Step 2. Install a certificate

You will need a SSL/TLS certificate installed to setup HTTPS connections.

For ones who don't have a certificate already, consider refer to [Let's Encrypt](https://letsencrypt.org/getting-started/). It's a nonprofit Certificate Authority which provides you free certificates.

Specifically, if you have shell access to your server and want a brand new certificate from Let's Encrypt, use the [ Certbot](https://certbot.eff.org/) ACME client. More specifically for Ubuntu users, please follow instructions [here](https://certbot.eff.org/instructions?ws=nginx&os=ubuntufocal).

Certbot can automatically override your Nginx configuration but we recommend not to do this, for we provide an all-in-one configuration in step 3.

_TLDR_:

For Ubuntu users:

```bash
snap install core; snap refresh core
snap install --classic certbot
ln -s /snap/bin/certbot /usr/bin/certbot
certbot certonly --nginx
```

If you really want to configure HTTPS servers by hand, please follow these [instructions](http://nginx.org/en/docs/http/configuring_https_servers.html).

### Step 3. Configure Nginx

Once you have Nginx and SSL certificates installed, it's time to add a server module to your nginx configuration.

Normally your Eldiron server will listen on port 3042, and your Eldiron client is connected to `/socket`. Thus you should proxy pass any requests to `/socket` to port 3042.

Here's a minimal example for this:

```nginx
upstream websocket {
        server 127.0.0.1:3042;
}

server {
        # Other configurations

        location /socket {
                proxy_pass http://websocket;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection $connection_upgrade;
                proxy_set_header Host $host;
        }
}
```

If Certbot didn't modify your Nginx configuration in step 2, you can simply copy the following configuration into a new file (eg. /etc/nginx/sites-enabled/eldiron). Dont't forget to replace `your.domain.com` with your domain name.

```nginx
map $http_upgrade $connection_upgrade {
        default upgrade;
        '' close;
}

upstream websocket {
        server 127.0.0.1:3042;
}

server {
        # SSL configuration
        #
        # listen 443 ssl default_server;
        # listen [::]:443 ssl default_server;
        #
        # Note: You should disable gzip for SSL traffic.
        # See: https://bugs.debian.org/773332
        #
        # Read up on ssl_ciphers to ensure a secure configuration.
        # See: https://bugs.debian.org/765782
        #
        # Self signed certs generated by the ssl-cert package
        # Don't use them in a production server!
        #
        # include snippets/snakeoil.conf;

        root /var/www/html;

        index index.html index.htm index.nginx-debian.html;
        server_name your.domain.com;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #       deny all;
        #}

        listen [::]:80;
        listen 80;

        listen [::]:443 ssl ipv6only=on;
        listen 443 ssl;
        ssl_certificate /etc/letsencrypt/live/your.domain.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/your.domain.com/privkey.pem;
        include /etc/letsencrypt/options-ssl-nginx.conf;
        ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

        location /socket {
                proxy_pass http://websocket;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection $connection_upgrade;
                proxy_set_header Host $host;
        }
}

server {
        if ($host = your.domain.com) {
                return 301 https://$host$request_uri;
        }

        listen 80;
        listen [::]:80;

        server_name your.domain.com;
        return 404;
}
```

Finally, restart Nginx:

```bash
systemctl reload nginx
```

Congratulations! You can now connect to your Eldiron server with a secure connection.

## Troubleshooting

### error: linker `cc` not found

This means that the Rust compiler can't find a C linker on your system. Please install one first (eg. gcc).

For Ubuntu users:

```bash
apt update
apt install build-essential
```
