# Flawless Hedgehog
An interactive Apache server hardening script.

The native configuration of Apache comes rather loose in terms of security, as it is one of the most used web server, a lot of people use it to serve their website, this is why I wanted to help them thighten their configuration by at least providing them a fast and easy way to add simple counter measures to potential threats.

It is made to help securing an out-of-the-box Apache server without having to go deep inside the configuration files.

Because it is intended to add a first layer of security rapidly, it avoid making too complex changes.

## Features
You have control on every action applied to your configuration.
The script features the most common best practices that should be applied to a web server that is exposed to the Internet, as following.

### Information leakage:
- Hide the Apache server signature on error pages
- Hide the Apache version in HTTP response headers
- Disable the Etag response header

### Exploration:
- Disable directory listing

### Authentication bypass:
- Restrict HTTP methods to GET, POST, HEAD

### [XSS](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)), [XST](https://www.owasp.org/index.php/Cross_Site_Tracing), [Clickjacking](https://www.owasp.org/index.php/Clickjacking):
- Add 'HttpOnly' and 'Secure' flags to all cookies emitted by the server
- Add header X-XSS-Protection to make browsers not load a page if a XSS attack is detected
- Disable Trace method
- Enable X-Frame-Options header and only allow iframes loading from the website domain

### DDoS (Slowloris):
- Decrease the Timeout setting from 300 to 60 seconds


## Usage
The script takes your Apache2 configuration path as parameter. If no parameter is given, `/etc/apache2/apache2.conf` is assumed.
```Shell
kamil@vps457979:~$ sudo chmod u+x
sudo flawless-hedgehog.sh [your Apache2 configuration path]
```

## Version of Apache tested
The script has been tested on the following versions of Apache:
- 2.4.25

## Disclaimer
Because it is intended to add a first layer of security rapidly, the script avoid making too complex changes that could interfer with upcomming modifications of your configuration, or system settings.

As it dont go deep in the hardening process, the script cant be trusted to make your server "flawless", although it should be enough for a first step in the process of making your web server more secure.
