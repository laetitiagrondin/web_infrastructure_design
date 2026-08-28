# 0. Model a Single-Server Web Stack

## *1. Server*

A server may be a physical machine or a virtual machine. It runs an operating system and is commonly hosted in a data center. The server is the machine itself, while the web server, application server, application code and database are services or software running on that machine.

## *2. DNS and A Record*

DNS translates the domain name `www.foobar.com` into an IP address so that the user can reach the server. In this scenario, the `www` record is an A record because it maps the domain name to the IPv4 address `8.8.8.8`.

## *3. Component Roles*

The web server (Nginx) receives HTTP requests and forwards them to the application layer. The application server runs the application, while the application code contains the logic used to process requests and generate responses. The database stores and retrieves the application's data.

## *4. Network Communication*

The user and the server communicate across a network using the TCP/IP protocol suite. TCP/IP provides the networking rules that allow requests to travel from the client to the server and responses to return to the client.

## *5. LAMP*

LAMP stands for Linux, Apache, MySQL and PHP. This design is LAMP-like because it combines a Linux-based server with a web server, application layer and database, but it is not a literal LAMP stack because it uses Nginx instead of Apache and does not require PHP.

## *6. Limitations*

The single server is a single point of failure because if it becomes unavailable, every service in the application becomes unavailable. Maintenance on this server can also cause downtime because there is no redundant server to handle requests. Finally, the capacity of one server is limited, so incresed traffic can eventually exceed its CPU, memory, network or other available resources.
