### Extra Configuration

In this section, we will discuss a little about the extra configurations for the app. They are not essential—at least to run locally. We are talking about DNS and the SSL certificate.

##### DNS (Domain Name System)

The **DNS** is basically a **contact book** used by your browser to check if the typed domain exists and retrieve its IP. To build this project, we used a virtual machine running a **Bind9** server to perform the function of a local **DNS**.

We configured **Bind9** to give the browser the **core app container** IP whenever it searched for the application domains (see [Installation](#installation)). It looks like this:

```$ORIGIN anatar.com.
$TTL 300;
@ IN SOA dns {email@domain.com}. (1 30 30 30 30);
@ IN NS dns
dns IN A {VM IP}
@ IN A {core app container IP}
web IN CNAME @
www IN CNAME @
```

##### SSL Certificate

To allow access to our application through the HTTPS protocol, obtaining an SSL certificate is necessary. It is a "virtual document" signed by an authority able to tell your browser that our site has a secure **HTTP** connection.

Considering that we did not intend to use our application publicly, acquiring a real certificate was not mandatory. Instead, we used a free program to generate and sign a certificate so we could "simulate" a real scenario. The program in question is called **easy-rsa**. 
