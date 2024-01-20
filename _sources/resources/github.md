# GitHub Interface reference    

This is an overview of the parts of GitHubt from the view on a repository page.  It has links to the relevant GitHub documentation for more detail. 

## Top of page
The very top menu with the {fa}`github` logo in it has GitHub level menus that are not related to the current repository. 

## Repository specific page

::::::::{tab-set}

::::::{tab-item} Code
**This is the main view of the project**

````{grid}
```{grid-item}
:columns: 9

Branch menu & info, file action buttons, download options (green code button)
```

```{grid-item}
:columns: 3

About has basic facts about the repo, often including a link to a documentation page
```


```{grid-item-card}
:columns: 9

File panel
+++
the header in this area lists who made the last commit, the message of that commit, the short hash, date of that commit and the total number of commits to the project. 

If there are actions on the repo, there will be a red x or a green check to indicate that if it failed or succeeded on that commit. 
^^^
file list: a table where the first column is the name, the second column is the message of the last commit to change that file (or folder) and the third column is when is how long ago/when that commit was made

```


```{grid-item}
:columns: 3

Releases, Packages, and Environments are optional sections that the repo owner can toggle on and off.  

[Releases](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) mark certain commits as important and give easy access to that version. They are related to [git tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

[Packages](https://docs.github.com/en/packages/learn-github-packages/introduction-to-github-packages) are out of scope for this course. GitHub helps you manage distributing your code to make it easier for users.  

[Environments](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment) are a tool for dependency management.  We will cover thigns that help you know how to use this feature indirectly, but probably will not use it directly in class.  This would be eligible for a build badge. 
```

```{grid-item-card}
:columns: 9


README file
```

```{grid-item}
:columns: 3

The bottom of the right panel has information about the languages in the project 
```
````

::::::


::::::{tab-item} Issues
a filterable list of [issues](https://docs.github.com/en/issues). the controls here hep you sort and find specific issues. 
the green button on the right helps you make a new issue.

By default it only shows open issues. to see closed ones, edit the text in the search box. 
::::::


::::::{tab-item} Pull Requests
A filter-able list of all the [pull requests](https://docs.github.com/en/pull-requests) in the repo. 

By default it only shows the open pull requests, to see merged and closed ones, edit the text in the search box. 
::::::


::::::{tab-item} Actions
This page allows you to run and view output from automatically run [GitHub Actions](https://docs.github.com/en/actions). 
::::::

::::::{tab-item} Projects
A list of all of the  projects linked to this repository and a button to add more. 
::::::


::::::{tab-item} Security
This tab tells you if code dependencies have had security issues reported.  This is out of scope for this course. GitHub's [code security](https://docs.github.com/en/code-security) features are  important when you are distributing code, but the particulars are language specific, so we will not discuss this much here. 

This could be a topic for an explore or build badge. 
::::::

::::::{tab-item} Insights
GitHub provides analysis of the activity in the repository. 
::::::


::::::{tab-item} Settings
You will only see this tab if you have admin rights on the repository.  This is where you can control high level things including: 
- add [collaborators](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-access-to-your-personal-repositories/inviting-collaborators-to-a-personal-repository)
- deploy a website with [GitHub Pages](https://docs.github.com/en/pages)

::::::

::::::::


