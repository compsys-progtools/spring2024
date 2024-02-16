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
This page is generated with code and calculations, you can view them for more precise implementations of what the English sentences mean. 
```


```{warning}
Some phrasing  on this may change, but the core of what is required will not change
```

````{margin}
```{tip}
You can expand the code below to see more detail in how the thresholds are calculated. 
```
````

```{code-cell} ipython3
:tags: [hide-input]

import os
from datetime import date,timedelta
import calendar
import pandas as pd
import numpy as np
import seaborn as sns

from myst_nb import glue
import plotly.express as px
# learning complexities
learning_weights = {'experience' :2, 'lab': 2, 'review': 3,'practice': 6,'explore': 9,'build' :36}
bonus_participation = 18
bonus_lab = 18
bonus_breadth = 32



# base grade influence cutoffs
thresh_mrw = {'D ':22*learning_weights['experience']+13*learning_weights['lab']+bonus_participation + bonus_lab, 
              'D+':22*learning_weights['experience']+13*learning_weights['lab']+bonus_participation + bonus_lab + 6*learning_weights['review'], 
              'C-':22*learning_weights['experience']+13*learning_weights['lab']+bonus_participation + bonus_lab + 12*learning_weights['review'], 
          'C ':22*learning_weights['experience']+13*learning_weights['lab']+18*learning_weights['review']+\
              bonus_participation + bonus_lab + bonus_breadth,
          'C+':22*learning_weights['experience']+13*learning_weights['lab']+bonus_participation + bonus_lab + bonus_breadth + 6*learning_weights['practice'] + 12*learning_weights['review'], 
          'B-':22*learning_weights['experience']+13*learning_weights['lab']+bonus_participation + bonus_lab + bonus_breadth + 6*learning_weights['review'] + 12*learning_weights['practice'], 
          'B ':22*learning_weights['experience']+13*learning_weights['lab']+18*learning_weights['practice']+\
              bonus_participation + bonus_lab + bonus_breadth,
          'B+': 22*learning_weights['experience']+13*learning_weights['lab'] +18*learning_weights['practice'] +\
              2*learning_weights['explore'] +bonus_participation + bonus_lab + bonus_breadth,
          'A-': 22*learning_weights['experience']+13*learning_weights['lab'] +18*learning_weights['practice'] +\
              4*learning_weights['explore'] +bonus_participation + bonus_lab + bonus_breadth,
          'A ': 22*learning_weights['experience']+13*learning_weights['lab'] +18*learning_weights['practice'] +\
              6*learning_weights['explore'] +bonus_participation + bonus_lab + bonus_breadth}

thresh_mrw
```

```{code-cell} ipython3
:tags: [hide-input]

examples_mrw = [[22,13,0,0,0,0],[22,13,18,0,0,0],[22,13,24,0,0,0],[24,13,18,6,0,0],
                [22,13,18,0,0,1],[26,13,0,18,0,0],[24,13,12,12,0,0],[24,13,0,24,0,0],
                [25,13,0,18,6,0],[25,13,0,18,4,0],[24,13,0,18,0,1],
                [22,13,18,0,0,3],[24,13,6,12,4,1],[24,13,12,6,2,2],[24,13,0,24,2,0]]

ex_df_mrw = pd.DataFrame(data=examples_mrw,columns = learning_weights.keys())
w_df_mrw = pd.DataFrame(data=[(ex_df_mrw[col]*learning_weights[col]) for col in learning_weights]).T.rename(columns=lambda col:col + '_weight')
w_df_mrw['total'] = w_df_mrw.sum(axis=1)
# [ex_df[col]*weights[col] for col in weights]
# columns = [col + '_weight' for col in weights ]
badge_thresh_df_mrw = pd.concat([ex_df_mrw,w_df_mrw],axis=1).reset_index()


ind_badges_mrw = [[exid,bt,bw,bc,1] for i,ex in enumerate(examples_mrw) for bc,(bt,bw) in zip(ex,learning_weights.items()) 
                                      for exid in bc*[i]]
per_badge_df_mrw = pd.DataFrame(ind_badges_mrw,columns=['example','badge','complexity','count','weight'])

# weight community badges, 


learning_df = pd.Series(learning_weights,name ='complexity').reset_index()
learning_df['badge_type'] = 'learning'
# comm_df  = pd.Series(community_weights,name='weight').reset_index()
# comm_df['badge_type'] = 'community'
# nans are for learning badges which all ahve weight 1
influence_df = learning_df.fillna(1).rename(columns={'index':'badge'})
# final df
influence_df['influence'] = influence_df['complexity']*influence_df['weight']
```


The total influence of each badge on the grade is as follows:

```{code-cell} ipython3
:tags: [hide-input]

# display
influence_df[['badge_type','badge','complexity','weight','influence']]
```

The total influence of a badge on your grade is the product of the badge's complexity.  All learning badges have a weight of 1, but have varying complexity.  

## Bonuses

In addition to the weights for each badge, there also bonuses that will automatically applied to your grade at the end of the semester.  These are for longer term patterns, not specific assignments.  You earn these while workng on other assignments, not separately. 

```{important}
the grade plans on the grading page and the thresholds above assume you earn the Participation and Lab bonuses for all grades a D or above and the Breadth bonus for all grades above a C.  
```

```{list-table}
:header-rows: 1

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
    - 6 review + practice submitted by 2/19 
    - 9
    - event
*   - Descriptive commits
    - all commits in KWL repo and build repos after penalty free zone have descriptive commit messages (not GitHub default or nonsense)
    - 9
    - event
*   - Community Star
    - 10 community badges
    - 18
    - auto
```

Auto bonuses will be calculated from your other list of badges.  Event bonuses will be logged in your KWL repo, where you get instructions when you meet the criteria. 

```{note}
These bonuses are not pro-rated, you must fulfill the whole requirement to get the bonus. Except where noted, each bonus may only be earned once
```

```{note}
You cannot guarantee you will earn the Git-ing unstuck bonus, if you want to intentionally explore advanced operations, you can propose an explore badge, which is also worth 9. 
```

## Grade thresholds


Grade cutoffs for total influence are:

```{code-cell} ipython3
:tags: [hide-input]

th_list = [[k,v] for k,v in thresh_mrw.items()]
pd.DataFrame(th_list, columns = ['letter','threshold']).sort_values(by='threshold').set_index('letter')
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

To calculate your final grade at the end of the semester, a script will count your badges and logged event bonuses. The script will output a dictionary with keys for each type of learning badge and event bonus with a count for the value of each. 

```{code-cell} ipython3
example_student = {'experience' :21, 'lab': 13, 'review': 6,'practice': 12,
                   'explore': 2,
                   'build' :1,
                 'community': 3,
                 'unstuck': 0,
                 'descriptive': 1,
                 'early': 1 }
```

Then these counts will go into the following function to calculate the final grade 

```{warning}
This is not complete, but will be before the end of the penalty free zone. 
```


```{code-cell} ipython3
# set up remaining constants (some are above)
bonus_criteria = {'participation_bonus': lambda r: int(r['experience'] >=22),
                  'lab_bonus':  lambda r: int(r['lab'] >=13),
                   'breadth_bonus': lambda r: int(r['review'] + r['practice']>=18),
                 'community_bonus': lambda r: int(r['community']>=10),
                 'unstuck_bonus': lambda r: r['unstuck'],
                 'descriptive_bonus': lambda r: r['descriptive'],
                 'early_bonus': lambda r: r['early'] }
bonus_values = {'participation_bonus': bonus_participation,
                  'lab_bonus':  bonus_lab,
                   'breadth_bonus': bonus_breadth,
                 'community_bonus': 18,
                 'unstuck_bonus': 9,
                 'descriptive_bonus': 9,
                 'early_bonus': 9 }
weights = learning_weights.copy()
weights.update(bonus_values)
community_thresh = {'experience':22,
                 'review':4,
                 'practice':7,
                 'review_upgrade':3}
community_cost = {'experience':3,
                 'review':4,
                 'practice':7,
                 'review_upgrade':3}

# compute grade

# def calculate_grade(badge_dict):
#     if badge_dict['community']>0:
        # apply community badges
        
    # add bonuses
    
    
    # final sum
    # sum([weights[cat]*count_dict[cat] for cat in count_dict.keys()])
```
