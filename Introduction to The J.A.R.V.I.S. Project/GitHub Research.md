# Table of Contents
1. [[#GitHub API]]
	1. [[#Getting Started]]
	2. [[#Forks]]
		1. [[#List of information]]
	3. [[#Stars]]
2. [[GitHub API Documentation]]
3. [[GitHub API Endpoints]]
4. [[How To Install The GitHub CLI]]
5. [[How To Setup The GitHub CLI]]





## GitHub API

### Table of Contents
1. [[#Getting Started]]
2. [[#Forks]]
	1. [[#List of information]]
3. [[#Stars]]

#### Getting Started

To start the GitHub API is very different compared to other API's due to needing to use the GitHub Command-Line-Interface(CLI) to gain something called an "GitHub API Token" this Token is only for the respective account that you have logged into the GitHub CLI ***(More on How to do that here: [[How To Setup The GitHub CLI]])***. To get your GitHub API Token you will need to run the command below:

>$ gh auth login

In any Terminal that has the GitHub CLI Installed ***(More on How to do that here: [[How To Install The GitHub CLI]])***. Follow the instructions that are given after the command above has been run. To then test the communication using your GitHub API Token you can run this command:

>$ gh api /octocat -method GET


#### Forks

To find who has forked your project/repository you can run this command:

>$ gh api -H "Accept: application/vnd.github+json" -H "X-GitHub-Api-Version:2022-11-28" /repos/{OWNER}/{REPO}/forks

This command will then pull the information of who has created a fork of that project/repository and when it was made. Along with a bunch of other information that it will always pull, here is a list of that data:

###### List of information:
- The Full Name of the Forked Repository.
- The User That Created It.
- The Time That it was Created.
- Whether it was made private or not.
- Tons of information on the owner of the forked repository.
- URL Links to the avatar of the owner and to their GitHub page.
- The List of every user to ever fork this repository
- The size of the forked repository.
- The branch that was forked.
- The current visibility of their project.
- The number of forks that they have.
- The number of open issues that they have.
- The number of watches that they have.
- The topics it's listed under.
- Whether it's archived or not.
- Whether it's been disabled or not.

To start with the implementation of the GitHub API within the J.A.R.V.I.S. Project, I need to install a python library called "PyGitHub" using this command:

>$ python -m pip install pygithub

This will then allow me to call the GitHub API through the use of python. To go this route you will need to make an app on GitHub that you ca have an api key for which you could then use with the PyGitHub python library. To call to the GitHub API, the base URL the api is calling to is as follows:

> https://www.github.com/Api/v3

This is the base form of the API and is what the python library is calling to. Son if I wanted to call directly from the API I would have to call it using this URL that looks like this for calling all forked data for the J.A.R.V.I.S. Project GitHub Repository:

> https://api.github.com/repos/Silewis37/jarvis/forks/

With headers that has the return format and the API key. This data is what is going to allow me to pull the data and information from the GitHub API and use it as I please, and It will also return in an untouched format so that way I am able to precisely pick and choose what values and information I wanted to pull from the API's response to my request. ***(For more information on the GitHub API endpoints go here: [[GitHub API Endpoints]] or Visit this Website: "https://pygithub.readthedocs.io/en/stable/apis.html")*** This was the only true way I could get all of this information here into a truly usable format. Since there are many other uses for the GitHub API it would be much of a waste not to discover more ways that I could possibly use this API to the advantage of the J.A.R.V.I.S. Project. And possibly have him be able to update his own programming in the future and download updates from the GitHub Repository all on his own so there would only be minimal effort from the end user.


#### Stars

The next use case that I have for the GitHub API in the J.A.R.V.I.S. Project is the use for looking at the Stars that are on a project. This is similar to the [[#Forks]] portion of this part of the project but it is calling to a different API Endpoint.