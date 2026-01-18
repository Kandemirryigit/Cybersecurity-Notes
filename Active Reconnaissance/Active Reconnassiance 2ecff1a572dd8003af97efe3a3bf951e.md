# Active Reconnassiance

# User-Agent Switcher and Manager

## Definition:

- **User-Agent Switcher and Manager** is a **browser extension** that allows you to **change (spoof) your User-Agent string**.

***A User-Agent identifies:***

- Browser type
- Browser version
- Operating system
- Device type
- Websites normally see this information in every HTTP request.

## Why User-Agent Switcher Is Used:

***It allows you to:***

- Test how websites behave for different devices
- Bypass weak User-Agent–based restrictions
- Detect bad server-side logic
- Avoid simple fingerprinting
- Simulate bots, mobile devices, or other browsers

# Wappalyzer:

## Definition:

- **Wappalyzer** is a **browser extension and online tool** used to **identify technologies used by websites**.

***It Detects:***

- Web frameworks
- Programming languages
- CMS
- JavaScript libraries
- Web servers
- Analytics & marketing tools

## Why Wappalyzer Is Important:

***Wappalyzer helps you:***

- Understand the **tech stack**
- Identify **potential attack vectors**
- Save time during reconnaissance
- Choose the right exploitation techniques

## Technologies Wappalyzer Can Detect:

- **Frontend**: React, Vue, Angular
- **Backend**: PHP, Node.js, Python, Java
- **CMS**: WordPress, Joomla, Drupal
- **Web Servers**: Apache, Nginx
- **Databases (indirect)**: MySQL, PostgreSQL
- **Analytics**: Google Analytics
- **CDN / Security**: Cloudflare

# traceroute command

## Definition:

- **`traceroute`** is a network diagnostic command used to **show the path (route)** that packets take from your machine to a target host.
- It reveals each **hop (router)** between you and the destination.

## Why traceroute Is Used:

***Traceroute helps to:***

- Understand network topology
- Identify intermediate routers
- Detect network bottlenecks
- Locate where packet loss or delay occurs
- Learn about ISPs and hosting providers

## What You Can Learn:

- Number of hops to the target
- IP addresses of routers
- Approximate physical distance
- Hosting provider information
- Network segmentation

# netcat command:

## Definition:

- **Netcat** is a powerful command-line networking tool used to **read from and write to network connections** using **TCP or UDP**.
- It is often called the **“Swiss Army knife of networking.”**

## Why Netcat Is Used:

***Netcat allows you to:***

- Test open ports
- Interact with network services manually
- Send and receive raw data
- Debug network services
- Transfer files
- Create simple servers or listeners

## Common netcat Uses:

### 1.Port Scanning:

- Check if a port is open.
- nc -zv [example.com](http://example.com/) 80
- `z` → scanning mode (no data sent)
- `v` → verbose output

### 2.Connecting to a Service:

- Manually interact with a service.
- nc [example.com](http://example.com/) 80
- Then type:
- GET / HTTP/1.1
Host: [example.com](http://example.com/)
- Useful for understanding server responses.

### 3.Banner Grabbing:

- Retrieve service banners.
- nc [example.com](http://example.com/) 21

***May reveal:***

- Service name
- Version info

### 4.Listening on a Port (Server Mode):

- Create a listener.
- nc -lvnp 4444
- `l` → listen mode
- `p` → port
- `n` → no DNS resolution
- `v` → verbose

### 5.File Transfer:

- Receiver: nc -lvnp 1234 > file.txt
- Sender: nc target_ip 1234 < file.txt

### Netcat vs Nmap

| Feature | Netcat | Nmap |
| --- | --- | --- |
| Scanning | Basic | Advanced |
| Manual interaction | Yes | No |
| Automation | Low | High |
| Service testing | Excellent | Limited |

##