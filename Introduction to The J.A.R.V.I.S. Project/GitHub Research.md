# Table of Contents
1. [[#GitHub API]]
	1. [[#Getting Started]]
	2. [[#Forks]]
2. [[GitHub API Documentation]]





## GitHub API

### Table of Contents
1. [[#Getting Started]]
2. [[#Forks]]


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

