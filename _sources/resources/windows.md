# Windows Help & Notes

## CRLF Warning 

This is GitBash telling you that git is helping.  Windows uses two characters for a new line `CR` (cariage return) and `LF` (line feed).
Classic Mac Operating system used the `CR` character.  Unix-like systems (including MacOS X) use only the `LF` character. 
If you try to open a file on Windows that has only `LF` characters, Windows will think it's all one line. To help you, 
since git knows people collaborate across file systems, when you check out files from the git database (`.git/` directory)
git replaces `LF` characters with `CRLF` before updating your working directory. 

When working on Windows, when you make a file locally, each new line will have `CRLF` in it. If your collaborator
(or server, eg GitHub) runs not a unix or linux based operating system (it almost certainly does) these extra 
characters will make a mess and make the system interpret your code wrong. To help you out, 
git will automatically, for Windows users, convert `CRLF` to `LF` when it adds
your work to the index (staging area). Then when you push, it's the compatible version. 

[git documentation of the feature](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration#Formatting-and-Whitespace) 

