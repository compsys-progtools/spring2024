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

# Detailed Grade Calculations 

```{important} 
This page is generated with code and calculations, you can view them for more precise implementations of what the english sentences mean. 
```

```{warning}
These calculations are going to change a little bit for spring 2024, will be posted before grade plans are do.  

What is on the [](grading.md) page will hold true, but the detailed calculation here will update a little bit in ways that provide some more flexibility. 
```

```{code-cell} ipython3
:tags: [hide-input]

# import os
# from datetime import date,timedelta
# import calendar
# import pandas as pd
# import numpy as np
# import seaborn as sns

# from myst_nb import glue
# import plotly.express as px
# learning complexities

from cspt import grade_constants, grade_calculation
```

Grade cutoffs for total influence are:

```{code-cell} ipython3
:tags: [hide-input]

grade_constants.letter_df
```

The total influence of each badge is as follows:

```{code-cell} ipython3
:tags: [hide-input]

# display
grade_constants.influence_df
```


In addition to the weights for each badge, there also bonuses that will automatically applied to your grade at the end of the semester.  These are for longer term patterns, not specific assignments.  You earn these while workng on other assignments, not separately. 

```{important}
the grade plans on the grading page and the thresholds above assume you earn the Participation and Lab bonuses for all grades a D or above and the Breadth bonus for all grades above a C.  

```

```{list-table}

*   - Name
    - Definition
    - Influence
    - type
*   - Participation
    - 22 experience badges
    - 18
    - auto
*   - Lab
    - 13 lab badges
    - 18
    - auto
*   - Breadth
    - If review + practice badges >-18:
    - 32
    - auto
*   - Git-ing unstuck 
    - fix large mistakes your repo using advanced git operations and submit a short reflection (allowable twice; Dr. Brown must approve)
    - 9
    - event
*   - Early bird
    - 6 review + practice submitted by 2/15 
    - 9
    - event
*   - Descriptive commits
    - all commits in KWL repo and build repos after penalty free zone have descriptive commit messages (not GitHub default or nonsense)
    - 9
    - event
*   - Curiosity
    - at least 10 experience reports have questions on time (before notes posted in evenings)
    - 9
    - event 
*   - Community Star
    - 10 community badges
    - 18
    - auto
*   - Hack the course
    - an explore or build that contributes to the course oss/website
    - 18
    - event
```

Auto bonuses will be calculated from your other list of badges.  Event bonuses will be logged in your KWL repo, where you get instructions when you meet the criteria. 

```{note}
These bonuses are not pro-rated, you must fulfill the whole requirement to get the bonus. Except where noted, each bonus may only be earned once
```

```{note}
You cannot guarantee you will earn the Git-ing unstuck bonus, if you want to intentionally explore advanced operations, you can propose an explore badge, which is also worth 9. 
```

## Bonus Implications

Attendance and participation is *very* important: 
- 14 experience, 6 labs, and 9 practice is an F
- 22 experience, 13 labs, and 9 practice is a C-
- 14 experience, 6 labs,  9 practice and one build is a C-
- 22 experience, 13 labs,  9 practice and one build is a C+


Missing one thing can have a nonlinear effect on your grade.
Example 1: 
- 22 experience, 13 labs, and 18 review is a C
- 21 experience, 13 labs, and 18 review is a C-
- 21 experience, 13 labs, and 17 review is a D+
- 21 experience, 12 labs, and 17 review is a D

Example 2:
- 22 experience, 13 labs, and 17 practice is a C
- 22 experience, 13 labs, 17 practice, and 1 review is a B-
- 22 experience, 13 labs, and 18 practice is a B

The Early Bird and Descriptive Commits bonuses are straight forward and set you up for success.  Combined, they are also the same amount as the participation and lab bonuses, so getting a strong start and being detail oriented all semester can give you flexibility on attendance or labs. 

Early Bird, Descriptive commits, Community Star, and Git-ing Unstuck are all equal to the half differnce between steps at a C or above. So earning any two can add a + to a C or a B for example:
- 22 experience, 13 labs, 18 practice, Descriptive Commits, and Early Bird is a B+  
- 22 experience, 13 labs, 18 review, Descriptive Commits, and Early Bird is a C+

in these two examples, doing the work at the start of the semester on time and being attentive throughout increases the grade without any extra work!

+++




If you are missing learning badges required to get to a bonus, community badges will fill in for those first.  If you earn the Participation, Lab, and Breadth bonuses, then remaining community badges will count toward the community bonus.  

For example, at the end of the semester, you might be able to skip some the low complexity learning badges (experience, review, practice) and focus on your high complexity ones to ensure you get an A. 

The order of application for community badges: 
- to make up missing experience badges 
- to make up for missing review or practice badges to earn the breadth bonus 
- to upgrade review to practice to meet a threshold 
- toward the community badge bonus 

+++

To calculate your final grade at the end of the semester, a script will count your badges and logged event bonuses. The script can output as a yaml file, which is like a dictionary, for an example here we will use a dictionary. 

see [cspt docs](https://compsys-progtools.github.io/courseutils/cli.html#cspt-grade) for CLI version

```{code-cell} ipython3
example_student = {'experience' :22, 'lab': 13, 'review': 0,'practice': 18,
                   'explore': 3,
                   'build' :0,
                 'community': 0,
                 'hack':0,
                 'unstuck': 0,
                 'descriptive': 1,
                 'early': 1,
                  'question':10 }
```

```{code-cell} ipython3
badges_comm_applied = grade_calculation.community_apply(example_student)
badges_comm_applied
```

```{code-cell} ipython3
grade_calculation.calculate_grade(badges_comm_applied)
```

```{code-cell} ipython3
grade_calculation.calculate_grade(badges_comm_applied,True)
```

```{code-cell} ipython3

```
