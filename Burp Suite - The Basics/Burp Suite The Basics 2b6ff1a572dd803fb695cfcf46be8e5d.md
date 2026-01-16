# Burp Suite: The Basics

# Burp suite

![Ekran görüntüsü 2025-11-25 195058.png](Ekran_grnts_2025-11-25_195058.png)

# What it is:

- **Burp Suite** is a **web application security testing tool**.
- It helps you **find vulnerabilities** in websites and web apps.
- It’s mostly used by **security researchers** and **ethical hackers**.
- It acts like a **proxy between your browser and the web server**, so you can intercept and analyze traffic.
- Burp Suite: A tool for analyizng,intercepting and manipulating http requests

# Burp Suite Editions:

## Community Edition (free):

- **Best for:** Learning, students, beginners

***Features:***

- Intercept HTTP/HTTPS requests
- Proxy (view & modify traffic)
- Repeater (manually resend requests)
- Decoder (encode/decode data)
- Comparer (compare requests/responses),

***Limitations:***

- No automated vulnerability scanning
- Intruder is **rate-limited (very slow)**
- No advanced extensions
- Manual testing only

- **Use case:**  Learn how web requests work and practice **manual penetration testing**

## Burp Suite Professional (Paid)

**Best for:** Professional pentesters, bug bounty hunters

***Features:***

- Everything in Community
- **Automated vulnerability scanner**
- Full-speed Intruder
- Advanced crawling
- Session handling rules
- Access to Burp Extensions (BApp Store)
- Better reporting

***Key advantage:***

- Can automatically find common vulnerabilities like:
- SQL Injection
- XSS
- CSRF
- Command Injection
- Directory traversal

- **Use case:**  Real-world web application security testing

## Burp Suite Enterprise Edition (Paid – Corporate)

- **Best for:** Large companies, DevSecOps teams

***Features:***

- Automated scanning of **many web apps**
- CI/CD pipeline integration
- Scheduled scans
- Centralized dashboard
- Continuous monitoring

***What it does NOT focus on:***

- Manual testing
- Request-by-request manipulation

- **Use case:** Continuous security scanning in enterprise environments

| Edition | Manual Testing | Auto Scan | Intruder Speed | Target User |
| --- | --- | --- | --- | --- |
| Community | ✅ Yes | ❌ No | ❌ Slow | Students |
| Professional | ✅ Yes | ✅ Yes | ✅ Fast | Pentesters |
| Enterprise | ❌ No | ✅ Yes | N/A | Companies |

# Main Features of Burp Suite

## 1.Proxy

- Intercepts HTTP/HTTPS requests and responses.
- Lets you **modify requests** before sending them to th9e server.

### Intercept is on:

- When **Intercept is ON**, Burp Suite **pauses** every HTTP/HTTPS request made by your browser **before it reaches the server**.
- When Intercept is ON, Burp Suite stops HTTP/HTTPS requests before they reach the server, allowing the tester to inspect and modify them.

### 1.) You open a website or click a button

- Your browser sends a request (GET, POST, etc.)

### 2.)Burp catches the request

- The request is **stopped** in the **Proxy → Intercept** tab
- The server does **not** receive it yet

### 3.)You have full control

- You can:
- View headers
- See parameters
- See cookies
- Modify data (URL, body, headers)

### 4.)You choose what happens next

- You click one of these:
- **Forward** → Send the request to the server
- **Drop** → Cancel the request completely
- **Edit** → Change the request before forwarding

### Websocket:

- **WebSocket** is a communication protocol that allows **real-time, two-way (bidirectional) communication** between a client (browser) and a server **over a single, persistent connection**.

***Traditional HTTP:***

- Client sends request
- Server sends response
- Connection closes
- Not real-time

***WebSocket:***

- Connection stays **open**
- Client **and** server can send data anytime
- Real-time

| HTTP | WebSocket |
| --- | --- |
| Request → Response | Two-way communication |
| Stateless | Persistent connection |
| Client-only initiation | Client & server can send |
| Not real-time | Real-time |

## 2.Scanner (Professional version)

- Automatically scans web apps for vulnerabilities (SQLi, XSS, etc.).

## 3.Repeater

- Lets you **send requests manually** multiple times.
- Good for testing input changes and seeing server responses.
- **Repeater** is a Burp Suite tool that allows you to **manually send the same HTTP/HTTPS request multiple times**, modify it, and **analyze the server’s response**.

### Why Repeater is used:

***Repeater is used to:***

- Test how a server reacts to **different inputs**
- Modify parameters, headers, cookies
- Debug application behavior
- Confirm vulnerabilities

***Unlike Intruder:***

- No automation
- Full control and precision

### How Repeater works:

***1.Capture a request***

- Intercept a request using **Proxy**
- Right-click → **Send to Repeater**

***2.Modify the request***

You can change:

- URL path
- Query parameters
- POST data
- Headers
- Cookies
- Authorization tokens

***3.Send the request***

- Click **Send**
- Request is sent to the server

***4.Analyze the response***

You see:

- Status code (200, 403, 500…)
- Response headers
- Response body
- Length & timing

You can repeat this **as many times as you want**.

### Common use cases

- Testing login logic
- Checking authorization (IDOR)
- SQL injection / XSS manual testing
- API testing
- Session and cookie manipulation

| Repeater | Intruder |
| --- | --- |
| Manual | Automated |
| One request at a time | Many payloads |
| Precise testing | Brute force / fuzzing |
| Best for learning | Best for scale |

## 4.Intruder

- Automates **brute-force attacks** or fuzzing.
- Can test login forms, parameters, or cookies.
- **Intruder** is a Burp Suite tool used to **automatically send many modified HTTP/HTTPS requests** in order to **test how an application handles different inputs**.
- Think of it as **automated attack / fuzzing tool**.

### Why Intruder is used

- Brute-force credentials
- Fuzz parameters
- Discover hidden inputs
- Test rate-limiting
- Find vulnerabilities automatically

### How Intruder Works:

***1.Capture a request:***

- Intercept a request (Proxy)
- Right-click → **Send to Intruder**

***2.Set attack positions:***

- Burp highlights parts of the request with `§`
- These are **injection points**
- You choose where payloads will be placed

***3.Choose attack type:***

- Intruder has **4 attack types**:

***Sniper:***

- One position at a time
- Most common
- Used for parameter testing

***Battering Ram:***

- Same payload in all positions
- Used when inputs must match

***Pitchfork:***

- Multiple payload lists, one-to-one mapping

***Cluster Bomb:***

- All combinations of payloads
- Most aggressive (very noisy)

***4.Configure payloads:***

Payloads can be:

- Wordlists
- Numbers
- Usernames
- Passwords
- Special characters
- Custom strings

***5.Start the attack:***

Intruder sends requests automatically and shows:

- Status codes
- Response length
- Response time
- Errors

| Intruder | Repeater |
| --- | --- |
| Automated | Manual |
| Many requests | One request |
| Fast testing | Precise testing |
| Fuzzing & brute-force | Logic testing |

## 5.Decoder

- Encode or decode data (Base64, URL, hex).

### What is decoder:

**Decoder** is a Burp Suite tool used to:

- **Encode** data
- **Decode** data
- **Transform** data between different formats
- It helps you understand **hidden, obfuscated, or encoded values** inside HTTP requests, responses, tokens, cookies, parameters, etc

### Why decoder is important:

Web applications often **encode data** to:

- Hide sensitive information
- Safely transmit data
- Prevent special-character issues

### Where Is Decoder Used:

You can use Decoder when:

- Inspecting **cookies**
- Analyzing **JWT tokens**
- Testing **URL parameters**
- Understanding **API payloads**
- Reversing **obfuscated values**

## 6.Comparer

- Compare two responses to find differences.

### What is Comparer:

***Comparer is a Burp Suite tool used to:***

- **Compare two pieces of data**
- Identify **differences and similarities**
- Highlight **exact changes** byte-by-byte or word-by-word

***It is mainly used to compare:***

- HTTP requests
- HTTP responses
- Tokens, cookies, headers
- Encoded or decoded values

## 7.Sequencer:

### What Is Sequencer:

***Sequencer is a Burp Suite tool used to:***

- **Analyze the randomness and unpredictability**
- of **session tokens, cookies, CSRF tokens, and other generated values**

***Its main goal is to answer:***

> ❓ Are these tokens secure and unpredictable?
> 

### Why Is Sequencer Important:

Web applications rely on **tokens** for security:

- Session IDs
- CSRF tokens
- Password reset tokens

If tokens are **predictable**, attackers can:

- Hijack sessions
- Bypass authentication
- Perform replay attacks

Sequencer helps detect **weak token generation**.

## 8.Extensions (BApp Store)

- Add custom functionality using **Java, Python, or JavaScript extensions**.
- Beyond the built-in features, the Java codebase of Burp Suite facilitates the development of extensions to enhance the framework's functionality
- These extensions can be written in Java, Python (using the Java Jython interpreter), or Ruby (using the Java JRuby interpreter).
- The **Burp Suite Extender** module allows for quick and easy loading of extensions into the framework, while the marketplace, known as the **BApp Store**, enables downloading of third-party modules.

## 9.Target

## What Is Target:

**Target** is the Burp Suite module used to:

- **Define what you are testing**
- **Organize application structure**
- **Control which traffic Burp focuses on**

In short:

> Target = scope + application map
> 

## Why Is Target Important:

Without Target:

- Burp captures **everything**
- You waste time analyzing irrelevant traffic
- You may test **out-of-scope** assets (dangerous in bug bounty)

Target helps you:

✔ Stay in scope

✔ Understand the app structure

✔ Focus attacks correctly

### Sıte Map:

- Automatically builds a **tree view** of the web application
- Shows:
    - Domains
    - Directories
    - Endpoints
    - Parameters
    - HTTP methods
    

### Scope

Scope defines:

- **Which hosts, URLs, and protocols are allowed**
- Everything else is considered **out of scope**

# Dashboard

## Tasks:

- The Tasks menu allows you to define background tasks that Burp Suite will perform while you use the application.
- In Burp Suite Community, the default “Live Passive Crawl” task, which automatically logs the pages visited, is sufficient for our purposes in this module.
- Burp Suite Professional offers additional features like on-demand scans.

## Event Log:

- The Event log provides information about the actions performed by Burp Suite, such as starting the proxy, as well as details about connections made through Burp.

## Issue Acticity:

- This section is specific to Burp Suite Professional.
- It displays the vulnerabilities identified by the automated scanner, ranked by severity and filterable based on the certainty of the vulnerability.

## Advisory:

- The Advisory section provides more detailed information about the identified vulnerabilities, including references and suggested remediations.
- This information can be exported into a report.
- In Burp Suite Community, this section may not show any vulnerabilities.

# Options

- let's explore the available options for configuring Burp Suite
- There are two types of settings: Global settings (also known as User settings) and Project settings.
- ***Global Settings:*** These settings affect the entire Burp Suite installation and are applied every time you start the application. They provide a baseline configuration for your Burp Suite environment.
- ***Project Settings:*** These settings are specific to the current project and apply only during the session. However, please note that Burp Suite Community Edition does not support saving projects, so any project-specific options will be lost when you close Burp.

# FoxyProxy

## What it is:

**FoxyProxy** is a **browser extension** (Firefox / Chrome) used to:

- Manage **proxy settings easily**
- Switch between **multiple proxies** with one click

In cybersecurity, it is mainly used to:

- Route browser traffic through **Burp Suite**