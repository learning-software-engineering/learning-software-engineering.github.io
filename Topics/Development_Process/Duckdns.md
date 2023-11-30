# Overcoming a Dynamic IP Address with DuckDNS

## Motivation

So you have chosen to deploy your application on AWS or perhaps you have turned a spare computer of yours into your home server. You are finally deployed and users can finally access your site! I mean, the address for your site may be something weird like `http://123.0.0.321` but at least _someone_ can access your site right? 

Well, if you ever have to restart your server to make updates or save some compute power when nobody is using your server, you may find that the next time you boot the server up, the IP address of your deployment has changed! Now you have to tell everyone your application has a new URL. Most hosting options (especially ones that are free) give your production server what is called a _Dynamic IP address_. In other words, services like AWS or your Internet Service Provider assign a new external IP address to your server whenever it boots up and joins the network. This is often done to save resources as an IP not used by one person, can be used by another.

While you could contact your hosting service or ISP to make it so that the external IP address of your server, which everyone connects to, stays fixed, this can either be quite a hassle or cost you money (something most students don't have to spare!). To get around this problem, one can turn to a _Dynamic DNS_ provider. A recent popular such provider among amateurs and hobbyists is a service called DuckDNS. 

## What is DuckDNS?

DuckDNS is a Dynamic Domain Name Service provider. In other words, they are a site that maps domain names to IP addresses. 