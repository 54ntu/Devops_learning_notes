# Important notes about <span color="red">NGINX.CONF</span> and forward proxy

# 📄 What does nginx.conf do?

<p>nginx.conf is the main configuration file for the NGINX web server. It defines how NGINX behaves in terms of: </p>


Key uses:

    1. Server configuration:

        --Which ports and IPs to listen on

        --Virtual hosts / server blocks

        --Domain-based routing (e.g., server_name example.com)

    2. Reverse proxy settings:

    --Forwarding client requests to backend services (like Node.js, Django, etc.)

    --Load balancing among multiple upstream servers


    3. ecurity:

    --TLS/SSL setup for HTTPS

    --Rate limiting, IP whitelisting, request filtering


    4. Performance:

    --Caching static content

    --Gzip compression

    --Connection limits


    5. Logging:

    --Access and error logs


    6. Custom URL routing:

    --Rewrite rules

    --Redirects (e.g., HTTP to HTTPS)


```js

NGINX

http {
    server {
        listen 80;
        server_name example.com;

        location / {
            proxy_pass http://localhost:3000;
        }
    }
}


```
<br>
<br>

# What is a Forward Proxy? How does it work?


A forward proxy sits between a client (usually inside a private network) and the public internet.
Purpose:

    -Hides the client's identity/IP from the server it is requesting

    -Controls outbound traffic

           -Censorship, filtering, or monitoring (e.g., parental controls, firewall rules)

    -Caching of frequently accessed resources

    -Bypass geo-restrictions or firewalls

How it works:

    -Client → Proxy → Internet

        --The client sends the request to the proxy (e.g., GET http://example.com).

    -Proxy fetches the data from the internet (on behalf of the client).

    -Proxy returns the response to the client.




<br><br>

# Forward Proxy vs Reverse Proxy
| Feature          | Forward Proxy              | Reverse Proxy                   |
| ---------------- | -------------------------- | ------------------------------- |
| Used by          | Clients                    | Servers                         |
| Protects         | Clients                    | Servers                         |
| Hides            | Client IP from server      | Server architecture from client |
| Common Tools     | Squid, NGINX (with config) | NGINX, Apache, HAProxy          |
| Example Use Case | Web filtering, VPN         | Load balancing, API gateway     |
