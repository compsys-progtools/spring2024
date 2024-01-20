# Tools and Resources

We will use a variety of tools to conduct class and to facilitate your programming.
You will need a computer with Linux, MacOS, or Windows. It is unlikely that a tablet 
will be able to do all of the things required in this course. A Chromebook may work, 
especially with developer tools turned on. Ask Dr. Brown if you need help getting access 
to an adequate computer.



All of the tools and resources below are either:

  - paid for by URI **OR**
  - freely available online.


## BrightSpace

````{margin}
```{note}
Seeing the BrightSpace site requires logging in with your URI SSO and being enrolled 
in the course
```
````

On BrightSpace, you will find links to other resource, this site and others. 
Any links that are for private discussion among those enrolled in the course 
will be available only from Brightspace.


## Prismia chat

Our class link for [Prismia chat](https://prismia.chat/) is available on Brightspace.
Once you've joined once, you can use the link above or type the url: prismia.chat.
We will use this for chatting and in-class understanding checks.

On Prismia, all students see the instructor's messages, but only the Instructor and 
TA see student responses. 

```{important}
Prismia is **only** for use during class, we do not read messages there outside of class time
```

You can get a transcript from class from Prismia.chat using the menu in the top right. 

## Course Website

The course website will have content including the class policies, scheduling, class notes,
 assignment information, and additional resources.
<!-- This will be linked from Brightspace and available publicly online at ). -->
Links to the course reference text and code documentation will also be included here in the assignments and class notes.

## GitHub

You will need a [GitHub](https://github.com/) Account. If you do not already have one, 
please [create one](https://github.com/signup) by the first day of class. If you have one, 
but have not used it recently, you may need to update your password and login credentials 
as the [Authentication rules](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/about-authentication-to-github) changed in Summer 2021.  


You will also need the [gh CLI](https://cli.github.com/). It will help with authentication
and allow you to work with other parts of github besides the core git operations. 

```{important}
You need to install this on Mac
```

<!-- In order to use the command line 
with https, you will need to [create a Personal Access Token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) for each device you use. In order to use the command line 
with SSH, set up your public key. -->



(programming-env)=
## Programming Environment

In this course, we will use several programming environments. In order to participate in class and complete assignments you need the items listed in the requirements list. The easiest way to meet these requirements is to follow the recommendations below. I will provide instruction assuming that you have followed the recommendations.
We will add tools throughout the semester, but the following will be enough
to get started.

```{warning}
This is not technically a *programming* class, so you will not need to know how
to write code from scratch in specific languages, but we will rely on programming
environments to apply concepts.
```

### Requirements:
- Python with scientific computing packages (numpy, scipy, jupyter, pandas, seaborn, sklearn)
- a C compiler
- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- A bash shell
- A web browser compatible with [Jupyter Notebooks](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/install.html#step-0-the-browser)
- nano text editor (comes with GitBash and default on MacOS)
- one IDE with git support (default or via extension)
- [the GitHub CLI](https://github.com/cli/cli#installation) on all OSs


### Recommendation

````{tab-set}

```{tab-item} Windows- option A

- Install python via [Anaconda](https://www.anaconda.com/products/individual) [video install ](https://www.youtube.com/watch?v=xxQ0mzZ8UvA)

- Git and Bash with [GitBash](https://gitforwindows.org/) ([video instructions](https://youtu.be/339AEqk9c-8)). 
```

```{tab-item} Windows - option B

Create a [bootable usb stick with Linux](https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#1-overview)

or use [windows subsystem for linux](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-11-with-gui-support#1-overview)

and then follow linux instructions

```

```{tab-item} MacOS
Video install instructions for Anaconda:
- Install python via [Anaconda](https://www.anaconda.com/products/individual) [video]](https://www.youtube.com/watch?v=TcSAln46u9U)
- install Git with the Xcode Command Line Tools. On Mavericks (10.9) or above you can do this by trying to run git from the Terminal the very first time.`git --version`

On Mac,  to install python via environment, [this article may be helpful](https://opensource.com/article/19/5/python-3-default-mac)


```


```{tab-item} Linux
- Install python via [Anaconda](https://www.anaconda.com/products/individual)

```



```{tab-item} Chrome OS

1. Find Linux (Beta) in your settings and turn that on.
2. Once the download finishes a Linux terminal will open, then enter the commands: `sudo
apt-get update` and `sudo apt-get upgrade`. These commands will ensure you are up to
date.
1. Install tmux with:

    ```
    sudo apt -t stretch-backports install tmux
    ```
2. Next you will install nodejs, to do this, use the following commands:

    ```
    curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash
    sudo apt-get install -y nodejs
    sudo apt-get install -y build-essential.
    ```
3. Next install Anaconda’s Python from the website provided by the instructor and use the
top download link under the Linux options.
1. You will then see a .sh file in your downloads, move this into your Linux files.
2. Make sure you are in your home directory (something like home/YOURUSERNAME),
do this by using the `pwd` command.
1. Use the `bash` command followed by the file name of the installer you just downloaded to
start the installation.
1. Next you will add Anaconda to your Linux PATH, do this by using the `vim .bashrc`
command to enter the .bashrc file, then add the `export
PATH=/home/YOURUSERNAME/anaconda3/bin/:$PATH` line. This can be placed at the
end of the file.
1.  Once that is inserted you may close and save the file, to do this hold escape and type `:x`,
then press enter. After doing that you will be returned to the terminal where you will then
type the source .bashrc command.
1.  Next, use the `jupyter notebook –generate-config` command to generate a Jupyter
Notebook.
1.  Then type `jupyter lab` and a Jupyter Notebook should open up.
```
````
<!-- (texteditor)=

````
- Text Editor: you may want a text editor outside of the Jupyter environment. Jupyter can edit markdown files (that you'll need for your portfolio), in browser, but it is more common to use a text editor like Atom or Sublime for this purpose. -->




## Zoom 

(backup only & office hours only)

[^tldr]: Too long; didn't read.

This is where we will meet if for any reason we cannot be in person. You will find the link to class zoom sessions on Brightspace.

URI provides all faculty, staff, and students with a paid Zoom account. It *can* run in your browser or on a mobile device, but you will be able to participate in office hours and any online class sessions if needed best if you download the [Zoom client](https://zoom.us/download) on your computer. Please [log in](https://uri-edu.zoom.us/) and [configure your account](https://uri-edu.zoom.us/profile).  Please add a photo (can be yourself or something you like) to your account so that we can still see your likeness in some form when your camera is off. You may also wish to use a virtual background and you are welcome to do so.  


For help, you can access the [instructions provided by IT](https://web.uri.edu/itservicedesk/zoom-at-uri/).
