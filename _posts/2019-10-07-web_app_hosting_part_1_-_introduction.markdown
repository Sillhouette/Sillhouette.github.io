---
layout: post
title:      "Web app Hosting: Part 1 - Introduction"
date:       2019-10-07 19:33:12 -0400
permalink:  web_app_hosting_part_1_-_introduction
---


### Table of Contents:

1. Introduction and choosing a Web Host
2. [Introduction to Web Servers, SSL, Web Caching, and Audits](http://)
3. [How to deploy a Rails app to Heroku](http://)
4. [How to deploy a Rails API with ReactJs front end to Heroku](http://)
5. [How to deploy a Rails App to a Digital Ocean Droplet](http://)
6. [How to deploy a Rails API with ReactJs front end to a Digital Ocean droplet](http://)


## Part 1 - Introduction

### How I got here
The last few weeks I have done a really deep dive on how to host a web application, specifically the portfolio projects that I made while I was going through the Flatiron curriculum and the portfolio website I made to showcase the projects. I found this to be a much more involved and complicated process than I anticipated and it took a ton of research and configuration for me to get everything set the way that I wanted it. 

I went through a couple iterations of hosting to figure out what served my purposes best. I want to go through my reasoning and how I settled on the configuration that I did. 

Here's what I was looking for in a host: 
* Run my apps without shutting down (Memory usage)
* Economically viable (Price)
* Allowed me to setup an SSL (Security)
* Documentation that I could use to get setup (Support system)

With this criterion in mind I set out to find a viable solution.

### Choosing a Web Host

Choosing a web host was a huge part of the battle. At first I just wanted to get my apps online, then as I went through the processes I figured out that there was more to what I wanted than I anticipated. The following is the journey that I took to get where I am now.

#### Heroku - Free Dynos

I started with Heroku, as it seems a lot of people do. I started doing a ton of research into how to host the different configurations of applications that I have. I did manage to get my apps hosted however I ran into the following problems:

* To run my rails app I needed to be able to have a database larger than 10,000 lines
* To run the same app I needed more computational power
* I could not have SSL on a free Dyno
* The Dyno goes to sleep after 30 mins of inactivity
* Boot time for the Dyno is up to 60 seconds after sleep

Some of these problems were huge problems that I needed to overcome, so I looked into the paid Hobby Dyno

#### Heroku - Hobby Dyno (Paid)

Cost: $9 per month, per dyno

When I realized that I didnt have enough space to store the data I needed for my Rails app, I decided to upgrade to the paid Hobby Dyno. This allowed me to host that app without the app going to sleep and needing to be rebooted. It also allowed me to use SSL, this is important because I was using OAuth with Facebook, and they require the authorization request to come from a secure website (https). The last benefit I had was that I was able to use a postgres database with up to 1 million lines in it, a significant improvement from the 10k lines you get with the free dyno. 

The cost of this was $9 per month per dyno. This meant that I was paying, just for this single app, $9/month.

At this point I had 3 apps hosted on heroku, my portfolio site on a free dyno, my streaming app on a free dyno,   and my trading card app on this paid dyno. 

I started running some tests on my trading card app, and quickly found out that the dyno it was hosted on crashed every time I tried to display the index of cards. This was unacceptable, so I started to dig into it and found that the loading of all of the cards for the index (40k+ cards) was too computationally expensive and was causing the dyno to crash and reboot. I only had 512MB of RAM on my dyno and this wasnt enough to store the index of cards to be displayed while the user was on the page. 

I later figured out that I was doing my pagination for these objects incorrectly and this caused a much bigger database query to be run then was necessary. This was the reason for the excess use of RAM and if I had solved this sooner, the app may have run just fine on this dyno. Before I dove into this and worked out a better way to do that I decided I needed to find a different host.

The last issue for me that wasnt resolved with Heroku was that my other two apps were still going to sleep after 30 mins of inactivity, and they couldnt use SSL. If I wanted to enable these features I would have to pay $9/month for each of these apps in adittion to upgrading my first dyno again to allow more computational power. This meant that to remain on heroku with my current need I would have to pay significantly more than $27/month. This was getting too expensive for me so I started looking for other web hosts. I started researching and came across two types of web hosts: Traditional hosts and Cloud hosts. The first type of hosting I looked at was traditional hosts.

#### Hostgator - (Paid)

Cost: $30 per month for a Virtual Private Server (VPS)

First I reached out to Hostgator and had an extended conversation with a sales rep who recommended to me that I host my apps on a Virtual Private Server (VPS). How that would work is that I would rent the vps from them, connect to it remotely and setup my apps to run, all on the same machine. I had some experience with VPSs before and knew that these servers were basically partitions on the same drive and I would be sharing a rented space with who knows how many other people. 

Despite that fact, I had put myself on a time crunch and was seriously considering the option. Talking to the sales rep I found out that they wanted $30 per month for me to rent this VPS. He also mentioned that they wanted me to pay for this up front, to get that price I would need to pay for 3 years of use, just over $1000. If I wanted to go monthly I could but the price jump was significant. 

Before I pulled the trigger on that I asked the rep for some time to figure out what exactly I wanted and how I would pay for it. He gave me to the end of the week. As I was working this out I decided to do some more research and see what else was out there. This is when I decided to look at cloud hosting more seriously.

#### Amazon Web Services (AWS) Paid

Cost: Unknown (Pay as you go, for what you use)

One of the cloud hosts I have heard a ton about was Amazon Web Services (AWS). I contacted their sales team to see if this would fit my needs and found that it might serve exactly what I was looking for. Cloud hosting basically means I could have my own linux server, whatever size I needed hosting my applications. This allows me to be a lot more flexible with my options, unlike the VPS mentioned earlier, I could start with something small and scale it up as needed. 

I started to dabble with some of the AWS infrastructure and researched trying to figure out which product would best fit my needs and ultimately could not land on one. There were multiple that seemed like they might fit my needs, but I couldnt figure out which one was best for me. 

I started up a lightsail server and worked with it a while to try to setup an app. I needed to do a ton of research into how to host a production server and struggled with it significantly. I decided that because I didnt know what I needed here, this was not the solution that best fit my needs.

#### Google Cloud (Paid)

Cost: Unknown (Pay as you go, for what you use)

I'll make this one short. My experience with Google Cloud wasnt as convoluted as AWS, they seemed to offer more straightforward services then AWS and I could work with it a bit easier. They also seemed to have a bit better support and documentation which helped me out. 

I managed to host one of my apps on Google Cloud but my biggest issue was still that I didn't know which of their products best fit me. The pricing model was complicated as they only charged for what I used but this created uncertainty for me in what I would be paying. I had heard about one other cloud host that I decided to check out and that's what I finally landed on. 

#### Digital Ocean (Paid)

Cost: $30 / Month (breakdown below)

The final cloud host I decided to check out was Digital Ocean. I heard about Digital Ocean from someone in the Flatiron graduates slack channel and decided to check them out. I set up a call with a sales rep to see if they could fill my needs. I learned with him that you can choose the memory, storage, and number of cores you think your app will need. You will be charged based on what you choose and you can upscale or downscale your app as needed. You can upgrade or downgrade if you only need to change the number of CPUs or the amount of memory (RAM) you need, but if you need to increase your storage you can only upgrade, there is no way to decrease the amount of storage on a droplet. 

These droplets start out at $5 per droplet for the smallest one and scale to extremely large proportions at 5$ intervals. You can get more information about the pricing from them directly.

The droplets are completely self-managed, so they cannot help you with the deployment of your server but they do have support systems in place. If you need help setting up the server they are happy to respond to questions about that with information from their FAQs, community guides, Digital Ocean guides, and similar questions that have been asked to the community. The most useful parts of their support structure I found were the community guides, Digital Ocean guides, and the community questions. Everything I needed to do either had a guide on how to do it or a question that was answered. 

Ultimately, this meant that I had great control over what I was getting, the pricing model was simple, scaling was easy, and it was self-managed which allowed me to configure the server however I saw fit. I would have to figure out how to deploy the applications myself but I was confident that with enough time and research I could manage it. I signed up and got started with deploying my applications. The details on how I went about it will be covered in a later blog post. 

### Conclusion

Like I said, this was a long process that involved a lot of research and playing with configurations. Here is an in depth look at what I wanted for each of my sites to recap:

Portfolio Website:
* Ability to host a React front end
* Ability to simultaneously host a Rails API
* Enough computational power to build the app
* Ability to configure Web Host software (Nginx)
* Ability to add SSL (HTTPS)
* Ability to server static files
* Ability to cache

MTG trading card site:
* Ability to deploy a Rails App in production mode
* Ability to configure Web Host software (Nginx)
* Ability to add SSL (HTTPS)
* Ability to server static files
* Ability to cache
* Enough computational power to run the app
* Enough space for the rather large database

Streaming app:
* Ability to host a React front end
* Ability to simultaneously host a Rails API
* Ability to configure Web Host software (Nginx)
* Ability to add SSL (HTTPS)
* Ability to cache
* Ability to host a separate server to handle the video streams

I was able to accomplish all of this by using Digital Ocean Cloud Hosting and configuring seperate droplets for each app, I have two $10 droplets for the MTG site and Portfolio site respectively, and two $5 droplets, one for the streaming website and a seperate one that runs the NodeJS RTMP server that handles the video streams. 
I am extremely happy with the amount and quality of documentation and community help found on Digital Ocean and I highly recommend using them if you are paying for a host. 

If you decide to go with them you can use the following link to sign up: [Sign up for $50 credit with Digital Ocean](https://m.do.co/c/e4868c71fe66 )
If you use my link you will get $50 of credit for the first month and you can use that time to work out how to host your own app or cancel your account if you dont like the service. 

Thanks for taking the time to read, in the next post for the series I will introduce you to web servers, SSL, and web caching and we can talk about why it's important. The rest of the series will go over how to deploy Rails and React/Rails apps to Heroku and Digital Ocean droplets. 

 - Austin
