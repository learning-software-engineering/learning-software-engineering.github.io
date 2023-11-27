# What is Nginx?

Nginx is the internet's traffic cop. Imagine you search for a website in your browser. Your request is sent accross the internet to that website's server. When the request reaches the website's server, it first has to go through Nginx. Nginx then directs your request to the correct place on the website's server, whether that might be querying a backend server like Django, fetching an image or other static content, or doing some other kind of task on the website's server. Nginx is really good at rerouting these requests really quickly, so that it can handle lots of requests at a time, keeping things moving quickly for everyone using the website. Nginx is essentially the middleman between the internet and a website.

<img src="https://miro.medium.com/max/1400/1*rFCyG1YbQwHWnadRIE0Ddg.png" alt="System Diagram With Nginx" width="500"/>

Nginx can do many things, like:

1. Serve web traffic over HTTPS
2. Load balance requests between multiple backend servers
3. Serve static content without a backend server like Django or Express

You can find a more exhaustive list on the [offical Nginx docs](https://nginx.org/en/)

# Installation and Setup

The installation processes varies depending upon your OS. It's most common to install Nginx on a Linux server, since this is what most of the cloud runs on. Here, we'll demonstrate how to install and setup Nginx on a cloud server running on Ubuntu 22.04. In case you want to install Nginx on Mac or Windows, try these tutorials:

- [Install Nginx on MacOS](https://nginxtutorials.com/install-nginx-on-mac/)
- [Install Nginx on Windows](https://medium.com/@chandramuthuraj/installing-nginx-on-windows-a-step-by-step-guide-6750575c63e2)

We assume that you have the following:

1. A cloud server running Ubuntu 22.04 accessible from the public internet
   - Digital Ocean is one of the simplest and most user friendly cloud providers. If you need help, checkout this [tutorial](https://docs.digitalocean.com/products/droplets/how-to/create/) on how to create a server on Digital Ocean!
   - Make sure you can connect to your server over ssh by uploading your ssh key to the server.
2. A domain name which points to your server
   - You can buy a domain and configure where it points through [NameCheap](https://www.namecheap.com/). If you need extra help, you can follow this great [YouTube tutorial](https://www.youtube.com/watch?v=95BC1b5FVps&ab_channel=codebubb) on how to point a NameCheap domain at a Digital Ocean server.

## Connecting to your server

In order to install Nginx on our server, we will first need to be connected to our server. Open a new terminal window and enter `ssh root@<your-server-ip>`, where `<your-server-ip>` is the IP address of your server. You should now be connected to your server.

## Install Nginx

On your server, run the following commands to refresh your server's package index, and install Nginx onto your server

```
sudo apt update
sudo apt install nginx
```

Now, configure your server's firewall to allow HTTP traffic via Nginx:

```
sudo ufw allow 'Nginx HTTP'
```

You can confirm HTTP traffic is now allowed with

```
sudo ufw status
```

The output should indicate that HTTP traffic is now allowed, like this:

<img width="470" alt="Screenshot 2023-11-22 at 1 05 44 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/36282235/a455f501-3f79-49da-84f3-c19747422de9">


When we installed Nginx with `apt`, the operating system should have started the Nginx service at the end of the installation process. We can confirm Nginx is running by entering:

```
systemctl status nginx
```

<img width="756" alt="Screenshot 2023-11-22 at 1 08 52 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/36282235/c5d42a9e-8c98-4310-a90c-9c265c26cf01">


If we ever need to restart or stop the Nginx service, we can do so with `systemctl restart nginx` and `systemctl stop nginx`.

Now, let's navigate to our server in the browser, and see what's there. Go to `http://yourdomain.com`, where `yourdomain.com` is the domain name you have pointed at your server. If all goes well, you should see the default Nginx landing page, letting you know that the web server is running!

![Nginx Landing Page](https://assets.digitalocean.com/articles/nginx_1604/default_page.png)

# Next Steps
Now that we have Nginx installed and running on our server, the possibilities are endless. Here's a few ideas:
1. To configure Nginx as a reverse proxy for an application server like Django or Express, try this [tutorial](https://www.digitalocean.com/community/tutorials/how-to-configure-nginx-as-a-reverse-proxy-on-ubuntu-22-04) from Digital Ocean explaining how to reverse proxy a simple Gunicorn server.
2. To serve static content like prebuilt websites or images using Nginx, try this excellent [tutorial](https://docs.nginx.com/nginx/admin-guide/web-server/serving-static-content/) from the official Nginx website on how to serve static content.
3. To secure Nginx with Let's Encrypt SSL and allow your websites to be accessed over HTTPS, try this [tutorial](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04) from Digital Ocean on how to set up secure SSL encryption with Nginx.
