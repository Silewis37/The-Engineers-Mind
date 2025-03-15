# Table of Contents
1. [[#GitHub API]]
	1. [[#Getting Started]]
	2. [[#Forks]]
		1. [[#List of information]]
	3. [[#Program Implementation]]
2. [[GitHub API Documentation]]
3. [[GitHub API Endpoints]]
4. [[How To Install The GitHub CLI]]
5. [[How To Setup The GitHub CLI]]





## GitHub API

### Table of Contents
1. [[#Getting Started]]
2. [[#Forks]]
	1. [[#List of information]]
3. [[#Program Implementation]]

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


#### Program Implementation

The next use case that I have for the GitHub API in the J.A.R.V.I.S. Project is the use for looking at the Stars that are on a project. This is similar to the [[#Forks]] portion of this part of the project but it is calling to a different API Endpoint. An Example of the headers for this request look something like this: 

> Headers: {
> 	"Accept": "application/vnd.github+json",
> 	"Authorization": "Bearer {TOKEN}",
> 	"X-GitHub-API-Version": "2022-11-28"
> }

Running the API by calling the process from the plugin that I created, the process that I created looks like this:


>def RepoForks(Owner, Repo):
  url = f"https://api.github.com/repos/{Owner}/{Repo}/forks"
  h = {
    "Accept": "application/vnd.github+json",
    "Authorization": f"Bearer {GithubAPI_TOKEN}",
    "X-GitHub-Api-Version": "2022-11-28"
  }
  response = requests.get(url, headers=h)
  print(response.json())
  with open("github-output.json", "w+") as f:
      data4 = json.dumps(response.json(), indent=4)
      f.write(data4)
      f.close()

File: src/plugins/connections/githubAPI.py
Ln: 31-43

This portion of the program is what allowed the J.A.R.V.I.S. Project to call out to the GitHub API and make a request for all the Fork Data on a single repository. I used it combined with the Settings Handler Plugin to make it so that the end user was able to switch between all of the data and select the owner and the repository that the J.A.R.V.I.S. Project would call out to and collect the data from. ***(More on the [[Settings Handler]])*** This was how I made it easier for the End-User to edit and control what data they pulled and they would also be able to manage it from within the application and not have to deal with looking at .json files and things of that nature. This will also allow the user to be able to better control the data that they wish to receive and here is how.

##### How The User Has Control

The user in this use case will have control due to the nature of the settings plugin and the way I have it configured. The backend connections settings JSON file looks something like this: 

>{
  "Github": {
      "Repository(s)": [
          {
              "Owner": "GITHUB USER",
              "Repo": "REPOSITORY NAME"
          },
          {
              "Owner": "GITHUB USER",
              "Repo": "REPOSITORY NAME"
          }
      ],
      "Forks": [
          {
              "Repo": "REPOSITORY NAME",
              "Active": true
          },
          {
              "Repo": "REPOSITORY NAME",
              "Active": false
          }
      ],
      "Starred": [
          {
              "Repo": "REPOSITORY NAME",
              "Active": true
          },
          {
              "Repo": "REPOSITORY NAME",
              "Active": false
          }
      ],
      "RepositoryCollaborators": [
          {
              "Repo": "REPOSITORY NAME",
              "Active": true
          },
          {
              "Repo": "REPOSITORY NAME",
              "Active": false
          }
      ],
      "Commits": [
          {
              "Repo": "REPOSITORY NAME",
              "Active": true
          },
          {
              "Repo": "REPOSITORY NAME",
              "Active": false
          }
      ],
      "RepositoryContributors": [
          {
              "Repo": "REPOSITORY NAME",
              "Active": true
          },
          {
              "Repo": "REPOSITORY NAME",
              "Active": false
          }
      ],
      "RepositoryDeployments": [
          {
              "Repo": "REPOSITORY NAME",
              "Active": true
          },
          {
              "Repo": "REPOSITORY NAME",
              "Active": false
          }
      ],
      "RepositoryTags": [
          {
              "Repo": "REPOSITORY NAME",
              "Active": true
          },
          {
              "Repo": "REPOSITORY NAME",
              "Active": false
          }
      ],
      "RepositoryIssues": [
          {
              "Repo": "REPOSITORY NAME",
              "Active": true
          },
          {
              "Repo": "REPOSITORY NAME",
              "Active": false
          }
      ],
      "RepositoryReleases": [
          {
              "Repo": "REPOSITORY NAME",
              "Active": true
          },
          {
              "Repo": "REPOSITORY NAME",
              "Active": false
          }
      ],
      "RepositoryCommitActivity": [
          {
              "Repo": "REPOSITORY NAME",
              "Active": true
          },
          {
              "Repo": "REPOSITORY NAME",
              "Active": false
          }
      ],
      "RepositoryTopics": [
          {
              "Repo": "REPOSITORY NAME",
              "Active": true
          },
          {
              "Repo": "REPOSITORY NAME",
              "Active": false
          }
      ],
      "RepositoryWatchers": [
          {
              "Repo": "REPOSITORY NAME",
              "Active": true
          },
          {
              "Repo": "REPOSITORY NAME",
              "Active": false
          }
      ],
      "Followers": true,
      "UserRepositories": true
  }
}

File: src/settings/connectionSettings.template.json
Ln: 1-135

This is what the GitHub portion of the Connection Settings JSON file looks like in some retrospect. This is what the User is changing when they change things from the interface side of the J.A.R.V.I.S. Project and all of this information is locally stored. The other information stored within this file is for database connection settings which are covered in a different section of The Engineers Mind. These settings are what allow the J.A.R.V.I.S. Project to call out to and gather data and information from the GitHub API. The J.A.R.V.I.S. Project is using this settings config file as the backbone of the connection settings and this is truly how it is managed for calling multiple items or having a list of multiple things that you would want to call for the J.A.R.V.I.S. Project to gather from like for example. Lets say I wanted to check on the J.A.R.V.I.S. Project's Number of forks and I also from time to time want to check on a different users repository activity at the same time. The end user can have it setup in such a way that the J.A.R.V.I.S. Project is able to call out to both project and pull all the data for it and it can be different for every connection setting listed in the above Code Chunk.

This is also how the J.A.R.V.I.S. Project gathers all the necessary items that are required to make the correct API calls and gather the correct information so that way the rest of the GitHub API plugin that I built can do its job and separate the data into useable data and information that will end up being displayed to the end user.