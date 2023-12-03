# What is Caddy?

[Caddy](https://caddyserver.com/) is a server written in Go with a focus on simplicity. All you need to run it is the executable, no dependencies required. While webservers like [Apache](https://httpd.apache.org/) and [Nginx](https://www.nginx.com/) are more mature and well documented, and can be more suited to large-scale deployments, Caddy can provide a great alternative for situations where the complexity of these solutions is either overkill or actively discouraged.

The most common use of Caddy is as a simple reverse proxy or webserver, which will be covered in this article, but it can get a lot more granular (e.g. [load balancing](https://caddyserver.com/docs/caddyfile/directives/reverse_proxy#load-balancing)) depending on your use case.

# Installation

Caddy can be run using a [downloaded executable](https://github.com/caddyserver/caddy/releases), but for best functionality you should use your preferred package manager. For example, on Debian or Ubuntu, using `sudo apt install caddy` will also install the `/etc/caddy/Caddyfile` config file, and a systemd service that you can use `systemd start caddy` to more robustly run in the background.


# Quick Start


## Simple Reverse Proxy
Caddy can be [used](https://caddyserver.com/docs/quick-starts/reverse-proxy) to manage requests made to your host

**Example**: Show your project running on port 9000 when you type `localhost` in your browser
```sh
caddy reverse-proxy --from :80 --to :9000
``` 

**Example**: 

## Simple File Server
Caddy can host a [file server](https://caddyserver.com/docs/quick-starts/static-files) to browse and access files from a public folder on your server. The below would allow access through your webbrowser at https://example.com (assuming you have the domain example.com directed to your host's ip using a registration service)
```sh
caddy file-server --root /srv --domain example.com --browse
```

Caddy can serve static websites (i.e. plain HTML/CSS/JS) by using a similar command as above
```sh
caddy file-server --root /srv --domain example.com
```


## Running with a Caddyfile
The following files will default to reading `/etc/caddy/Caddyfile`. A different location can be specified using the `--config` flag. Full documentation can be found at https://caddyserver.com/docs/command-line

[`caddy validate`](https://caddyserver.com/docs/command-line#caddy-validate)

- Checks a config file for errors

[`caddy run`](https://caddyserver.com/docs/command-line#caddy-run)

- Runs Caddy in the foreground (i.e. without giving the shell back)

[`caddy start`](https://caddyserver.com/docs/command-line#caddy-start) and [`caddy stop`](https://caddyserver.com/docs/command-line#caddy-stop)

- Runs Caddy in the background (i.e. will give back the shell after starting)
 
While there do exist [ways](https://caddyserver.com/docs/config-adapters) to tackle caddy configuration using other formats, the most common (and easiest) way to do so is through the [Caddyfile](https://caddyserver.com/docs/caddyfile). All configuration you'll ever need to do can be done through it, though you can always keep different aspects of what you're doing in separate files and [import](https://caddyserver.com/docs/caddyfile/directives/import) them as necessary.

---

*This is assuming your frontend is being served on port 8080 and your backend on port 9000* 

**Example**: Serving API and frontend from the same machine but different subdomains
```s
# No port specified will default to port 80 for HTTP
# And port 443 for HTTPS 
example.com {
        reverse_proxy localhost:8080
}

api.example.com {
        reverse_proxy localhost:9000
}
```

**Example**: Serving API from specific path
```s
example.com {
    # Caddy will stop at the first match

    # * indicates that it is not an exact path, 
    # and to enable partial-matching
    reverse_proxy /api/* localhost:9000

    # no path given is equivalent to *, in other words a catch-all
    reverse_proxy localhost:8080
}
``` 

# Going Farther with the Caddyfile

## Syntax
The Caddyfile is written in its own syntax which is similar to a mix between [YAML](https://github.com/abiosoft/caddy-yaml) and [JSON](https://caddyserver.com/docs/json/) (Both of which can be used instead if desired), but will not be covered by this guide

### Global Options Block
A curly-brace block with nothing before it is used for **global options**, and will apply to everything else in your configuration.
```s
{
    # Caddy by default will handle HTTPS certificates renewal and redirecting HTTP to HTTPS,
    # but in a development environment this might not be what we want, so this option will turn
    # those features off
    auto_https off
}
```
```s
{
    # Alternatively, we could have everything served by internal local certs
    # https://caddyserver.com/docs/caddyfile/directives/tls#internal
    local_certs
    tls internal
}
```
---
### Addresses

In the context of a Caddyfile, an Address is the part of what is specifically being requested by the requestor (e.g. what is entered into a web browser URL bar, or what is provided by the `Host` header of an HTTP request) that identifies the host, and can be simplified in a few ways. The following are all valid addresses by Caddy per [the documentation](https://caddyserver.com/docs/caddyfile/concepts#addresses):

- `localhost`
- `example.com`
- `:443` (omitted hostname/IP is treated as `localhost`)
- `http://example.com`
- `localhost:8080`
- `127.0.0.1`
- `[::1]:2015`
- `*.example.com`
- `http://` (will match all HTTP requests)
 
As you can see, the protocol (HTTP vs HTTPS) and port (`:8080`) can be specified

#### Single Address in File

When using Caddy to serve content from a single Address, e.g. `localhost`, no brackets around the options are required. Simply type your Address at the top of the file, and list options (known as [directives](https://caddyserver.com/docs/caddyfile/directives)) line by line.

**Example**: Caddyfile version of the Simple File Server
```s
# Any desired global options can go here
{
}

# address by which to access Caddy
# will respond to HTTP (port 80) and HTTPS (port 443) by default
localhost 

# Brackets ARE needed to specify multiple arguments to individual directives. 
file_server {
    
    # sets the file_server to serve from this folder
    root * /srv 

    # hides hidden folders in the root directory (but not sub-folders)
    hide .*

    # instructs Caddy to generate and serve 
    # a browsable index of files rather than 
    # making our own 
    browse
}

```