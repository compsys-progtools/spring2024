---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.10.3
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# KWL Chart

(kwlworkflows)=
## Working with your KWL Repo

```{important}
The `main` branch should only contain material that has been reviewed and approved by the instructors.
```

````{margin}
```{tip}
You could apply branch protections on your feedback branch if you like
```
````


1. Work on a specific branch for each activity you work on
1. when it is ready for review, create a PR from the item-specifc branch to `main`.
1. when it is approved, merge into main.



(kwlmin)=
## Minimum Rows




```
# KWL Chart


<!-- replace the  _ in the table or add new rows as needed -->

| Topic | Know | Want to Know | Learned |
| ------| ------- | ------ | ------- |
| Git | _ | _ | _ |
| GitHub | _ | _ | _ |
| Terminal | _ | _ | _ |
| IDE | _ | _ | _ |
| text editors | _ | _ | _ |
|file system | _ | _ |_ |
|bash | _ | _ | _ |
|abstraction | _ | _ | _ |
|programming languages | _ | _ | _ |
|git workflows | _ | _ | _ |
| git branches | _ | _ | _ |
| bash redirects | _ | _ | _ |
|number systems | _ | _ | _ |
| merge conflicts | _ | _ | _ |
| documentation | _ | _ | _ |
| templating | _ | _ | _ |
|bash scripting | _ | _ | _ |
| developer tools | _ | _ | _ |
| networking | _ | _ | _ |
|ssh | _ | _ | _ |
| ssh keys | _ | _ | _ |
|compiling | _ | _ | _ |
| linking   | _ | _ | _ |
| building | _ | _ | _ |
| machine representation  | _ | _ | _ |
| integers   | _ | _ | _ |
| floating point  | _ | _ | _ |
|logic gates | _ | _ | _ |
| ALU | _ | _ | _ |
| binary operations | _ | _ | _ |
| memory | _ | _ | _ |
| cache | _ | _ | _ |
| register | _ | _ | _ |
| clock | _ | _ | _ |
| Concurrency | _ | _ | _ |
```



## Required Files

This lists the files for reference, but mostly you can keep track by badge issue checklists. 


```{code-cell} ipython3
:tags: ["remove-input"]

import pandas as pd

check_df = pd.read_csv('../kwl.csv')

# FIXME: update grade free dates
# penalty_free_dates = ['2022-01-24','2023-01-26']
# #bonus_dates = ['2022-12-05','2022-12-07','2022-12-12']
# gz = {True:'penalty-free',False:'full-requirements'}
# zoner = lambda d: gz[d in penalty_free_dates]
# check_df['zone'] = check_df['date'].apply(zoner)

check_df.sort_values(by='date').style.hide(axis="index")
``` 

<!-- 
-->

<!-- 
bonus = {True:'bonus',False:'single'}
zoner = lambda d: gz[d in grade_free_dates]
check_df['zone'] = check_df['date'].apply(zoner) -->