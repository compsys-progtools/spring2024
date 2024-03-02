# Build Badges 

Build may be individual or in pairs. 

## Proposal Template

If you have selected to do a project, please use the following template to propose a bulid

```{literalinclude} ../_worksheets/build_proposal.md
```


The deliverables will depend on what your method is, which depend on your goals. It must be approved and the final submitted will have to meet what is approved.  Some guidance:
- any code or text should be managed with git (can be GitHub or elsewhere)
- if you write any code it should have documentation
- if you do experiments the results should be summrized
- if you are researching something, a report should be 2-4 pages, plus unlimited references in the 2 column [ACM format.](https://www.acm.org/publications/proceedings-template)

This guidance is generative, not limiting, it is to give ideas, but not restrict what you *can* do.


## Updates and work in Progress

These can be whatever form is appropriate to your specific project. Your proposal should indicate what form those will take.


## Summary Report


This summary report will be added to your kwl repo as a new file `build_report_title.md` where `title` is the (title or a shortened version) from the proposal.  

This summary report have the following sections.  
1. **Abstract** a one paragraph "abstract" type overview of what your project consists of.  This should be written for a general audience, something that anyone who has taken up to 211 could understand. It should follow guidance of a scientific abstract.
1. **Reflection** a one paragraph reflection that summarizes challenges faced and what you learned doing your project
1. **Artifacts** links to other materials required for assessing the project.  This can be a public facing web resource, a private repository, or a shared file on URI google Drive. 

## Collaborative Build rules/procedures

- Each student must submit a proposal PR for tracking purposes. The proposal may be shared text for most sections but the deliverables should indicate what each student will do (or be unique in each proposal). 
- the proposal must indicate that it is a pair project, if iteration is required, I will put those comments on both repos but the students should discuss and reply/edit in collaboration
- the project must include code reviews as a part of the workflow links to the PRs on the project repo where the code reviews were completed should be included in the reflection
- each student must complete their own reflection.  The abstract can be written together and shared, but the reflection must be unique. 


## Build Ideas 


### General ideas to write a proposal for 
- make a [vs code extension](https://code.visualstudio.com/api/get-started/your-first-extension) for this class or another URI CS course
- port the courseutils to rust. [crate clap](https://docs.rs/clap/latest/clap/) is like the python click package I used to develop the course utils
- buld a polished documentation website for your CSC212 project with [sphinx](https://devblogs.microsoft.com/cppblog/clear-functional-c-documentation-with-sphinx-breathe-doxygen-cmake/) or another static site generator 
- use version control, including releases on any open source side-project and add good contributor guidelines, README, etc 

### Auto-approved proposals

For these build options, you can copy-paste the template below to create your proposal issue and assign it to `@brownsarahm`.

For working alone there are two options, for working with a partner there is one. 

#### 212 Project Solo- Docs focus

Use this option if your team for your 212 project is not currently enrolled in this class or does not want to do a collaborative build. This version focuses on the user docs.


```
## 212 Project Doc & Developer onboarding

Add documentation website and developer onboarding information to your CSC 212 project. 

### Objectives

<!-- in this section describe the overall goals in terms of what you will learn and the problem you will solve. this should be 2-5 sentences, it can be bullet points/numbered or a paragraph  -->

This project will provide information for a user to use the data structure implemented for a CSC 212 project and for a potential collaborator to add new features to it. The information will live in the repo and be served as a rendered website. 

### Method

 <!-- describe what you will do , will it be research, write & present? will there be something you build? will you do experiments?-->
1. ensure there is API level documentation in the code files
1. build a documentation website using [jupyterbook/ sphinx/doxygen/] that includes setup instructions and examples
1. configure the repo to automatically build the documentation website each time the main branch is updated


### Deliverables


- link to repo with the contents listed in method in the reflection file


### Milestones

<!-- give a target timeline -->

```

#### 212 Project Solo- Developer focus

Use this option if your team for your 212 project is not currently enrolled in this class or does not want to do a collaborative build. This version focuses on the contributor experience. 


```
## 212 Project Doc & Developer onboarding

Add documentation website and developer onboarding information to your CSC 212 project. 

### Objectives

<!-- in this section describe the overall goals in terms of what you will learn and the problem you will solve. this should be 2-5 sentences, it can be bullet points/numbered or a paragraph  -->

This project will provide information for a user to use the data structure implemented for a CSC 212 project and for a potential collaborator to add new features to it. The information will live in the repo and be served as a rendered website. 

### Method

 <!-- describe what you will do , will it be research, write & present? will there be something you build? will you do experiments?-->

1. ensure there is API level documentation in the code files
1. add a license, readme, and contributor file
1. add [code tours](https://marketplace.visualstudio.com/items?itemName=vsls-contrib.codetour) that help someone understand how the data strucutre works and learn how to contribute 
1. set up a PR template
1. set up 2 issue templates: 1 for feature request and 1 for bug reporting


### Deliverables


- link to repo with the contents listed in method in the reflection file


### Milestones

<!-- give a target timeline -->

```

#### 212 Project Pair

Use this option if your teammate for your 212 project is in this class and wants to do a collaborative build. 


```
## 212 Project Doc & Developer onboarding

Add documentation website and developer onboarding information to your CSC 212 project. 

### Objectives

<!-- in this section describe the overall goals in terms of what you will learn and the problem you will solve. this should be 2-5 sentences, it can be bullet points/numbered or a paragraph  -->

This project will provide information for a user to use the data structure implemented for a CSC 212 project and for a potential collaborator to add new features to it. The information will live in the repo and be served as a rendered website. 

### Method

 <!-- describe what you will do , will it be research, write & present? will there be something you build? will you do experiments?-->
1. ensure there is API level documentation in the code files
1. build a documentation website using [jupyterbook/ sphinx/doxygen/] that includes setup instructions and examples
1. configure the repo to automatically build the documentation website each time the main branch is updated
1. add [code tours](https://marketplace.visualstudio.com/items?itemName=vsls-contrib.codetour) that help someone understand how the data strucutre works and learn how to contribute 
1. set up a PR template
1. set up 2 issue templates: 1 for feature request and 1 for bug reporting



### Deliverables


- link to repo with the contents listed in method in the reflection file


### Milestones

<!-- give a target timeline -->

```



<!-- 
## Project Examples
- One type of project would be to do a research project on a topic we cover in class and create a .md file with your findings that demonstrates your knowledge of the topic. The .md file would include an **Abstract**, **Body**, **Reflection** including what you did and what you learned from it, and a **Bibliography**. Potential research topics include:
    - Motherboards
    - CPUs: Their History, Evolution, and How They Work
    - GPUs: A Graphics Card That Revolutionized Machine Learning
    - The Differences Between Operating Systems: MacOS vs Windows VS Linux
    - Abstraction For Dummies: Explaining Abstract Concepts to the Layman
- Another type of project could be to create a program using the tools taught in class to maintain the program. What would be included in this would be a .md reporting your findings that demonstrates an understanding of the tools used and a link to the repository hosting the program including **documentation** written for the program.
 -->
