---
jupytext:
  formats: ipynb,md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.15.1
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# Schedule



## Overview

The following is a tentative outline of topics in an order, these things will be filled into the concrete schedule above  as we go.  These are, in most cases bigger questions than we can tackle in one class, but will give the general idea of how the class will go.  

<!-- This plan accounts for 1 less week than we actually have.  We will either go over somewhere or we'll use the last week for sharing projects, reflection, or an additional topics that comes up during the semester. -->

### How does this class work?

*one week*

We'll spend the first two classes introducing some basics of GitHub and setting expectations for how the course will work. This will include how you are expected to learn in this class which requires a bit about how knowledge production in computer science works and getting started with the programming tools.  

<!-- ### How do all of these topics relate?

*approximately two weeks*

````{margin}
```{tip}
We will integrate history throughout the whole course.  Connecting ideas to
one another, and especially in a sort of narrative form can help improve retention of ideas. My goal is for you to learn.  

We'll also come back to different topics multiple times with a slightly different framing each time.  This will both connect ideas, give you chance to practice recalling (more recall practice improves long term retention of things you learn), and give you a chance to learn things in different ways.
```
````

We'll spend a few classes doing an overview where we go through each topic in a little more depth than an introduction, but not as deep as the rest of the semester. In this section, we will focus on how the different things we will see later all relate to one another more than a deep understanding of each one.  At the end of this unit, we'll work on your grading contracts.

We'll also learn more key points in history of computing to help tie concepts together in a narrative.


Topics:
- bash
- man pages (built in help)
- terminal text editor
- git
- survey of hardware
- compilation
- information vs data -->

(sectools)=
### What tools do Computer Scientists use?



Next we'll focus in on tools we use as computer scientists to do our work.  We will use this as a way to motivate how different aspects of a computer work in greater detail. While studying the tools and how they work, we will get to see how some common abstractions are re-used throughout the fields and it gives a window and good motivation to begin considering how the computer actually works.     

Topics:
- bash
- linux
- git
- i/o
- ssh and ssh keys
- number systems
- file systems


### What Happens When I run code?


Finally, we'll go in really deep on the compilation and running of code. In this part, we will work from the compilation through to assembly down to hardware and then into machine representation of data.   

Topics:
- software system and Abstraction
- programming languages
- cache and memory
- compiliation
- linking
- basic hardware components


## Recommended workload distribution

```{note}
General badge deadlines are on the [detailed badge procedures](badges) page. 
```


To plan your time, I recommend expecting the following:
- 30 minutes, twice per week for prepare work (typically not this much). 
- 1.5(review)-3(practice) hours, twice per week for the dated badges (including revisions). 

````{margin}
```{note}
the first explore or build will probably take longer than this because there will be more revisions, but the later ones will likely take less than this
```
````

For each explore: 
- 30 min for proposal
- 7 hours for the project

For each build: 
- 1.5 hour for the proposal (including revisions)
- 22 hours for the project
- 30 min for the final reflection

This is a four credit course, meaning we have approximately 4 hours of class + lab time per week($75 \times 2+105 = 255$ minutes or 4.25 hours). By the [accredidation standards](https://www.neche.org/wp-content/uploads/2018/12/Pp111_Policy_On_Credits-And-Degrees.pdf), students should spend a minimum of 2 hours per credit of work outside of class over 14 weeks.  For a 4 credit class, then, the expected minimum number of hours of work outside of class you should be spending is 112 hours(2 * 4 * 14). With these calculations, given that there are 26 class sessions and only 18 review or practice are required, it is possible to earn an A with approximately 112 hours of work outside of class and lab time.  

## Tentative Timeline

```{warning}
This section is not yet updated for spring 2024. 

This is a rough example. 
```

This is the planned schedule, but is subject to change in order to adapt to how things go in class or additional questions that come up. 

```{code-cell} ipython
import pandas as pd
pd.read_csv('schedule.csv',index_col='date').sort_index()
```

## Tentative Lab schedule

```{code-cell} ipython
pd.read_csv('labschedule.csv',index_col='date').sort_index()
```
