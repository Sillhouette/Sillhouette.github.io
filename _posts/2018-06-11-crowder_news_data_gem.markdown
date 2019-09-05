---
layout: post
title:      "CLI Data Gem: Getting Started"
date:       2018-06-11 20:00:52 -0400
permalink:  crowder_news_data_gem
---


The CLI data gem project is something I've been looking forward to since I started the course. My first main project, it was very exciting to arrive here. I had a bit of trouble with the previous two labs but nothing that couldnt be resolved with some help from the amazing technical coaches. 

I went to start this project by watching the walkthrough that was provided in the lab. I followed along with it for a while until it came to a point where I realized I wasn't able to save anything. This was frustrating because they ask us to create a brand new project for the CLI lab but the instructions on how to do that with the IDE were nowhere to be found. I ended up habing to reach out with the ask a question to have someone help me learn how to start a new project with the IDE. 

Here is how it's done:

First you open your IDE, whether it's the desktop one or the browser one, it shouldn't matter: 

[![Fresh IDE](https://i.imgur.com/b9kUrxK.png)](https://i.imgur.com/b9kUrxK.png)

Then you need to type some commands into the terminal:

Bundling your gem project:
* Type "bundle gem project_name" To create a file structure
* Press "enter/return"
* Type "y" to add a liscence to your program
* Type "y" to add a code of conduct to your program
* Type "cd ./project_name" to go into your new project directory
* Type "git init" which initiates the git in your project

[![Fresh IDE](https://i.imgur.com/PJAX5SQ.png)](https://i.imgur.com/PJAX5SQ.png)

Now you have a fresh project in the IDE to work with. We just need to connect that project to github so it can be saved in their servers and accessed at any time. This is IMPORTANT because the learn IDE works on the Learn servers and does not save any work locally. That means if you disconnect from their servers it is likely you lose any work that was not previously pushed to github. Here is how to add your new project to github:

Here is what you do on GitHub:

* Log into github and click "Start a new project"

[![Starting new project](https://i.imgur.com/embLgAR.png)](https://i.imgur.com/embLgAR.png)

* Enter your project name and an (optional) description then hit create project

[![Defining new Project](https://i.imgur.com/CL6r9yS.png)](https://i.imgur.com/CL6r9yS.png)

* Then go back to your IDE and type "git add ." to add your project to add the files to be commited to git.
* Type "'git commit -m "message for first commit"' to get your commit ready to be pushed to github
*  Then go back to the project on github and copy the two lines of code that are highlighted in the next picture:

[![Copying Links](https://i.imgur.com/EigdY3j.png)](https://i.imgur.com/EigdY3j.png)

* Paste those commands into the terminal to connect github to your local project and push your files to github.

[![pushing the files to guthub](https://i.imgur.com/WRy90KB.png)](https://i.imgur.com/WRy90KB.png)

* Refresh your github page and you should see your files in there:

[![Checking Files on GitHub](https://i.imgur.com/3acZB9C.png)](https://i.imgur.com/3acZB9C.png)

A couple notes:

Like I said before, if you don't do this you risk losing any work you do due to not having your own local enviroment set up. If you need to take a break from your work thats fine, just make sure you push any changes you made to github like this:

* Type "git add ." to get all of your altered files ready to commit
* Type "git commit -m "commit message contents" to commit them to git
* Type "git push" to push the files to your github

If you leave your work after you've pushed it to github and want to start working on it again, it's simple to retrieve:

* Go to your project in github and click the "Clone/Download" button and Copy the ssh link they provide:

[![Clone Button](https://i.imgur.com/S7ZqXHU.png)](https://i.imgur.com/S7ZqXHU.png)

* Open your fresh IDE, whether desktop or browser and type "git clone git@github.com:Sillhouette/project_name.git" where that url is the url of your project rather than mine

[![Clone Button](https://i.imgur.com/dpznJxe.png)](https://i.imgur.com/dpznJxe.png)

After you get your fresh project set up I highly reccomend starting off by following along with Avi as he walks you through the project on this video:

[Avi CLI Tutorial](https://www.youtube.com/watch?v=_lDExWIhYKI)

It's super important to at least perform some of the actions he starts off with there in his video to get the project under way. 

I hope this helped and good luck to you all!

Until next time
- Richard Austin Melchior
