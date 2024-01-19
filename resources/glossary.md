# Glossary

```{tip}
Contributing glossary terms or linking to uses of glossary terms to this page is eligible for community badges
```

```{glossary}

absolute path
  the path defined from the root of the system

add (new files in a repository)
  the step that stages/prepares files to be committed to a repository from a local branch

bash
  bash or the bourne-again shell is the primary interface in UNIX based systems

bitwise operator
  an operation that happens on a bit string (sequence of 1s and 0s). They are typically faster than operations on whole integers. 


branch
  a copy of the main branch (typically) where developmental changes occur. The changes do not affect other branches because it is isolated from other branches.

Compiled Code
  code that is put through a compiler to turn it into lower level assemlby language before it is executed. must be compiled and re-executed everytime you make a change.


directory
  a collection of files typically created for organizational purposes


fixed point number
  the concept that the decimal point does not move in the number. Cannot represent as wide of a range of values as a floating point number.


floating point number
  the concept that the decimal can move within the number (ex. scientific notation; you move the decimal based on the exponent on the 10). can represent more numbers than a fixed point number.

git
  a version control tool; it's a fully open source and always free tool, that can be hosted by anyone or used without a host, locally only.


GitHub
  a hosting service for git repositories


.gitignore
  a file in a git repo that will not add the files that are included in this .gitignore file. Used to prevent files from being unnecessarily committed.


git objects
  FIXME something (a file, directory) that is used in git; has a hash associated with it


git Plumbing commands
  low level git commands that allow the user to access the inner workings of git.


git Workflow
  a recipe or recommendation for how to use Git to accomplish work in a consistent and productive manner


HEAD
  a file in the .git directory that indicates what is currently  checked out (think of the current branch)


merge
  putting two branches together so that you can access files in another branch that are not available in yours

mermaid
  meraid syntax allows user to create precise, detailed diagrams in markdown files.

hash function
  the actual function that does the hashing of the input (a key, an object, etc.)


hashing
  putting an input through a function and unique fixed length output (the output is called a hash; used in hash tables and when git hashes commits). 

  
integrated development environment
  also known as an IDE, puts together all of the tools a developer would need to produce code (source code editor, debugger, ability to run code) into one application so that everything can be done in one place. can also have extra features such as showing your file tree and connecting to git and/or github.


interpreted code
  code that is directly executed from a high level language. more expensive computationally because it cannot be optimized and therefore can be slower.
  
issue
  provides the ability to easily track ideas, feedback, tasks, or bugs. branches can be created for specific issues. an issue is open when it is created. pull requests have the ability to close issues.


Linker
  a program that links together the object files and libraries to output an executable file.
  
path
  the "location" of a file or folder(directory) in a computer

pull (changes from a repository)
  download changes from a remote repository and update the local repository with these changes.

pull request
  allow other users to review and request changes on branches. after a pull request recieves approval you can merge the changed content to the main branch.

push (changes to a repository)
  to put whatever you were working on from your local machine onto a remote copy of the repository in a version control system.

relative path
  the path defined **relative** to another file or the current working directory; may start with a name, includes a single file name or may start with `./`

repository
  a project folder with tracking information in it in the form of a .git directory in it


ROM (Read-Only Memory)
  Memory that only gets read by the CPU and is used for instructions


SHA 1
  the hashing function that git uses to hash its functions (found to have very serious collisions (two different inputs have same hashes), so a lot of software is switching to SHA 256)

sh
  abbr. see shell

shell
  a command line interface; allows for access to an operating system


ssh 
  allows computers to safely connect to networks (such as when we used an ssh key to clone our github repos)


templating
  templating is the idea of changing the input or output of a system. For instance, the Jupyter book, instead of outputting the markdown files as markdown files, displays them as HTML pages (with the contents of the markdown file).


terminal
  a program that makes shell visible for us and allows for interactions with it


tree objects
  type of git object in git that helps store multiple files with their hashes (similar to directories in a file system)

yml
    see YAML

[YAML](https://yaml.org/)  
    a file specification that stores key-value pairs. It is commonly used for configurations and settings. 


```
