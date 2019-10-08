---
layout: post
title:      "Web App Hosting: Part 2 - Web Servers, SSL, Web Caching, and Audits"
date:       2019-10-08 11:46:16 -0400
permalink:  web_app_hosting_part_2_-_web_servers_ssl_web_caching_and_audits
---


### Table of Contents:

1. [Introduction and choosing a Web Host](https://www.austinmelchior.com/blog/2)
2. Introduction to Web Servers, SSL, Web Caching, and Audits
3. [How to deploy a Rails app to Heroku](http://)
4. [How to deploy a Rails API with ReactJs front end to Heroku](http://)
5. [How to deploy a Rails App to a Digital Ocean Droplet](http://)
6. [How to deploy a Rails API with ReactJs front end to a Digital Ocean droplet](http://)

### Web Hosting Peripherals

As I looked into web hosting I found there is a number of things over and above just programming the application that should be done. First off, I noticed after I got my sites hosted that chrome was flagging them as *insecure*. This caused my Oauth login for Facebook on one of my apps to break as Facebook requires that you send the authorization request from an HTTPS protected domain. After doing some more research I figured that in order to configure an SSL it would be best to start out with a web server. The web server would manage the ports, serve up my application no matter the configuration, and manage web caching as well. While I was researching I also became intrigued by the audits section of the chrome console. This auditing tool processes your site and gives you a score in performance, accessibility, best practices, and site engine optimization. Lets take a look at each of these technologies and tools in a little more depth.

### Web Servers

Web server technology is software that is designed to handle incoming web traffic. The main purpose of a web server is to store and transfer web site data upon the request of a visitor’s browser. Modern web servers are designed to handle a number of different requests including but not limited to serving website front ends, handling requests to backend web servers, handling email clients, and serving up static files to a user for download. There are many web servers out there to choose from including Apache, Nginx (pronounced `engine-x` , and Microsoft's Internet Information Server (IIS). We will be taking a look at Nginx and the benefits that it provides.

#### Traffic Routing and Reverse Proxying

The main purpose of a web server is to route http traffic to different files on a server. Nginx provides a platform that allows users to route traffic in a vast array of configurations. Nginx is also a reverse proxy, which is defined as the following:

>A proxy server is a go‑between or intermediary server that forwards requests for content from multiple clients to different servers across the Internet. A reverse proxy server is a type of proxy server that typically sits behind the firewall in a private network and directs client requests to the appropriate backend server. A reverse proxy provides an additional level of abstraction and control to ensure the smooth flow of network traffic between clients and servers.

This reverse proxy provides a number of benefits allowing for load balancing, web acceleration in the form of caching, and SSL encryption. These capabilities give us flexibility and security in how we manage our web traffic. 

When we dive into actually deploying our application to the world we will be using Nginx to handle:

1. Routing client traffic to our client
2. Routing requests from our client to our backen
3. Configuring SSL encryption
4. Enabling HTTP2 protocol
5. Compressing files for faster service
6. Handling web caching for better user experience
7. Serving up static files for viewing or download

Setting up the configurations for the web server to handle each of these things is not too difficult, it just takes a bit of research and patience.  

For more information about Nginx you can visit their wiki page here: 
[Nginx Wiki](https://www.nginx.com/resources/wiki/)
For more information about reverse proxys check out this resource:
[Reverse Proxy Server](https://www.nginx.com/resources/glossary/reverse-proxy-server/)

### Secure Socket Layers (SSLs)

According to [SSL.com](https://www.ssl.com/faqs/faq-what-is-ssl) SSL is defined as:

>SSL (Secure Sockets Layer) and its successor, TLS (Transport Layer Security), are protocols for establishing authenticated and encrypted links between networked computers. Although the SSL protocol was deprecated with the release of TLS 1.0 in 1999, it is still common to refer to these related technologies as “SSL” or “SSL/TLS.” The most current version is TLS 1.3, defined in RFC 8446 (August 2018).

The most common and well-known use of SSL/TLS is secure web browsing via the HTTPS protocol. This provides a number of benefits such as: 

* Authenticating that the server you are visiting is in possesion of the private key that matches the public key served in the certificate on the client. 
* Ensuring that the web pages being acccessed have not been altered by a third party before the request gets to the server
* Encryption of the communications between the client and the server

This allows users of your application to easily recognize that your site has the appropriate encryption to handle sensitive data such as credit card information, login credentials, and social security numbers. Modern clients are designed to make it apparent whether or not a client is connected to an application with an SSL by displaying a padlock in the address bar, showing an HTTPS connection, and warning the user if they are connected to an insecure web address. 

Obtaining an SSL is quickly becoming common practice for all sites, there is a huge push to get every site on the web protected by these. There are many certificate authorities (CAs) that provide the service of generating these SSL certificates. Each certificate has an expiration date and needs to be renewed at some point in the future by a Certificate Authority. Most certificate authorities charge for their services, however, there are a few that dont such as [Certbot](https://certbot.eff.org/). This is the CA we will be using to generate the certificate for the apps we will host later on in this series.

For more in depth information about SSLs You can take a look at the following FAQ: [What is SSL](https://www.ssl.com/faqs/faq-what-is-ssl/)

### Web Caching

Web caching is the extremely valuble practice of storing client files on a client (browser) to reduce server lag. Here's how Wikipedia defines it:

>A Web cache (or HTTP cache) is an information technology for the temporary storage (caching) of Web documents, such as Web pages, images, and other types of Web multimedia, to reduce server lag. A Web cache system stores copies of documents passing through it; subsequent requests may be satisfied from the cache if certain conditions are met.

Web caching is important because it greatly enhances user experience by storing files so that load times are reduced. This allows the client to serve up a web page without having to request all of the files from the server, enabling quicker load times and even offline loading of a site. This is especially useful with a single page app like a React app that doesnt rely on communication with the server to work. We will handle web caching using Nginx's web cache capabilities, we will go over how this works in Part 5 and Part 6 of this series. 

If you want to dive into this topic more, here is a community tutorial written by a user at Digital Ocean:
[Web Caching Basics: Terminology, HTTP Headers, and Caching Strategies](https://www.digitalocean.com/community/tutorials/web-caching-basics-terminology-http-headers-and-caching-strategies)

### Audits

Website audits are extremely valuble tools that enable us to analyze our application to see what we need to do to provide an ideal user experience, and optimize our site for search engine visibility. 

>Website audit is a full analysis of all the factors that affect website’s visibility in search engines. This standard method gives a complete insight into any website, overall traffic and individual pages. Website audit is completed solely for marketing purposes. [Wikipedia](https://en.wikipedia.org/wiki/Website_audit)

There are many auditing tools out on the web and each of them have their benefits, but by far the easiest and most accessible one (for Chrome users) is located right in Google Chrome's inspection suite. This audit tool analyzes a web page based on the following factors:

* Performance
* Accessibility
* Best Practices
* Site Engine Optimization

This allows us to take a critical look at the design of our website and make necessary changes to optimize it in a number of ways. 

The performance audit looks at the load times of your web page and gives you a score based on how fast (or slow) the page loads. Slower connection speeds can also be simulated so that you can see how fast your page loads on devices that may not have the best internet connections, such as phones connected to the 4G network. The tool also gives you a ton of suggestions on how to improve your load times by pointing out explicitly what affects the times the most, and how you can fix it. I've found that the best thing you can do to improve load times is to enable caching, and be sure to use images that are in modern formats, and sized appropriately to fit the need of the page. 

The accessibility audit is designed to analyze a web page and point out different problems with the accessibility of the site. It uses a set of accessibility guidelines that can be accessed by clicking on the *learn more* link provided when a problem is pinpointed. This checks things like mobile button sizes, color contrasts, and alternate images for image elements. This is important to pay attention to as it allows us to provide a phenomenal UI experience.

The best practices audit checks your web page to ensure that you are following a number of best practices such as using HTTPS connections, HTTP2 protocols, allowing passwords to be pasted into fields, and a number of other things that ensure the user has a safe and pleasant experience. 

The search engine optimization audit checks your page to see if it has a number of elements that search engines look for when looking to rank your page for search results. Some of these elements include the document having a `title` element, the document containing appropriate `meta` tags, and whether or not the page has a successful HTTP status code. These things are extremely important if you want your site to be on the front page of search engine results so that you can be seen by the world.

Now that we have a little more information about the different technologies that we can use to enchance our application in a number of different ways, lets get into the fun stuff, how to host various applications on Heroku, and Digital Ocean. 

- Austin
