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
community_weights = {'experience_replace' :3,  'review_replace': 4,'practice_replace': 7, 'review_upgrade': 3,}
bonus_participation = 18
bonus_lab = 18
bonus_breadth = 32
bonus_early = 9



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


# thresh_mrw
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


# delta = thresh_mrw['C ']-thresh_mrw['D ']
# minus_thresh = {k.strip()+'-':int(v-delta/3) for k,v in thresh_mrw.items()}
# minus_thresh

# plus_thresh = {k.strip()+'+':int(v+delta/3) for k,v in thresh_mrw.items()}

# calculate the final thresholds for all leter grades
# thresh_mrw.update(minus_thresh)
# thresh_mrw.update(plus_thresh)
# thresh_mrw.pop('A+');
# thresh_mrw.pop('D-');

ind_badges_mrw = [[exid,bt,bw,bc,1] for i,ex in enumerate(examples_mrw) for bc,(bt,bw) in zip(ex,learning_weights.items()) 
                                      for exid in bc*[i]]
per_badge_df_mrw = pd.DataFrame(ind_badges_mrw,columns=['example','badge','complexity','count','weight'])

# weight community badges, 


learning_df = pd.Series(learning_weights,name ='complexity').reset_index()
learning_df['badge_type'] = 'learning'
# comm_df  = pd.Series(community_weights,name='weight').reset_index()
# comm_df['badge_type'] = 'community'
# nans are for learning badges which all ahve weight 1
influence_df = pd.concat([learning_df]).fillna(1).rename(columns={'index':'badge'})
# final df
# influence_df['influence'] = influence_df['complexity']*influence_df['weight']
influence_df
```

Grade cutoffs for total influence are:

```{code-cell} ipython3
:tags: [hide-input]

th_list = [[k,v] for k,v in thresh_mrw.items()]
letter_df = pd.DataFrame(th_list, columns = ['letter','threshold']).sort_values(by='threshold').set_index('letter')
letter_df
```

```{code-cell} ipython3
# +1*learning_weights['review']+ bonus_participation + bonus_lab  +bonus_breadth
14*learning_weights['experience']+7*learning_weights['lab']+12*learning_weights['practice'] +\
learning_weights['build'] 
# + bonus_participation + bonus_lab 

```

The total influence of each badge is as follows:

```{code-cell} ipython3
:tags: [hide-input]

# display
influence_df[['badge_type','badge','complexity','weight','influence']]
```


The total influence of a badge on your grade is the product of the badge's complexity.  All learning badges have a weight of 1, but have varying complexity.  


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

To calculate your final grade at the end of the semester, a script will count your badges and logged event bonuses. The script will output a dictionary with keys for each type of learning badge and event bonus with a count for the value of each. 

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
# set up remaining constants (some are above)
exp_thresh = 22
rp_thresh =18
bonus_criteria = {'participation_bonus': lambda r: int(r['experience'] >=exp_thresh),
                  'lab_bonus':  lambda r: int(r['lab'] >=13),
                   'breadth_bonus': lambda r: int(r['review'] + r['practice']>=rp_thresh),
                 'community_bonus': lambda r: int(r['community']>=10),
                 'unstuck_bonus': lambda r: r['unstuck'],
                 'descriptive_bonus': lambda r: r['descriptive'],
                 'early_bonus': lambda r: r['early'] ,
                 'hack_bonus': lambda r: r['hack'] ,
                 'curiosity_bonus': lambda r: r['question']>10}
bonus_values = {'participation_bonus': bonus_participation,
                  'lab_bonus':  bonus_lab,
                   'breadth_bonus': bonus_breadth,
                 'community_bonus': 18,
                 'hack_bonus':18,
                 'unstuck_bonus': 9,
                 'descriptive_bonus': 9,
                 'early_bonus': 9 ,
                 'curiosity_bonus': 9 }
weights = learning_weights.copy()
weights.update(bonus_values)
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

```{code-cell} ipython3
# apply community badges if needed
if example_student['experience'] < exp_thresh and example_student['community']>0:
    experience_needed = exp_thresh - example_student['experience']
    community_needed = experience_needed*community_cost['experience']
    if example_student['community'] >=community_needed:
        example_student['community'] -= community_needed
        example_student['experience'] += experience_needed

rp_sum = example_student['review'] + example_student['practice']
if rp_sum <18:
    # doing this lazy instead of a loop
    if example_student['community'] >= community_cost['practice']:
        example_student['community'] -= community_cost['practice']
        example_student['practice'] += 1
    if example_student['community'] >= community_cost['practice']:
        example_student['community'] -= community_cost['practice']
        example_student['practice'] += 1
    if example_student['community'] >= community_cost['review']:
        example_student['community'] -= community_cost['review']
        example_student['review'] += 1
    if example_student['community'] >= community_cost['review']:
        example_student['community'] -= community_cost['review']
        example_student['review'] += 1
    if example_student['community'] >= community_cost['review']:
        example_student['community'] -= community_cost['review']
        example_student['review'] += 1


# apply bonuses 
example_student.update({bname:bfunc(example_student) for bname,bfunc in bonus_criteria.items()})
# compute final
influence = sum([example_student[k]*weights[k] for k in weights.keys()])
influence
letter_df[letter_df['threshold']<=influence].iloc[-1].name.strip()
```

```{code-cell} ipython3
example_student
```

```{code-cell} ipython3

```
