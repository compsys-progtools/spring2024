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
weights_mrw = {'experience' :2,'review': 3,'practice': 6,'explore': 9,'build' :36}
# base grade influence cutoffs
thresh_mrw = {'D ':22*weights_mrw['experience'], 'C ':22*weights_mrw['experience']+18*weights_mrw['review'],
          'B ':22*weights_mrw['experience']+18*weights_mrw['practice'],
          'A ': 22*weights_mrw['experience']+18*weights_mrw['practice'] + 6*weights_mrw['explore']}

examples_mrw = [[22,0,0,0,0],[23,18,0,0,0],[22,24,0,0,0],[24,18,6,0,0],
                [22,18,0,0,1],[26,0,18,0,0],[24,12,12,0,0],[24,0,24,0,0],
                [25,0,18,6,0],[25,0,18,4,0],[24,0,18,0,1],
                [22,18,0,0,3],[24,6,12,4,1],[24,12,6,2,2],[24,0,24,2,0]]

ex_df_mrw = pd.DataFrame(data=examples_mrw,columns = weights_mrw.keys())
w_df_mrw = pd.DataFrame(data=[(ex_df_mrw[col]*weights_mrw[col]) for col in weights_mrw]).T.rename(columns=lambda col:col + '_weight')
w_df_mrw['total'] = w_df_mrw.sum(axis=1)
# [ex_df[col]*weights[col] for col in weights]
# columns = [col + '_weight' for col in weights ]
badge_thresh_df_mrw = pd.concat([ex_df_mrw,w_df_mrw],axis=1).reset_index()


delta = thresh_mrw['C ']-thresh_mrw['D ']
minus_thresh = {k.strip()+'-':int(v-delta/3) for k,v in thresh_mrw.items()}
minus_thresh

plus_thresh = {k.strip()+'+':int(v+delta/3) for k,v in thresh_mrw.items()}

# calculate the final thresholds for all leter grades
thresh_mrw.update(minus_thresh)
thresh_mrw.update(plus_thresh)
thresh_mrw.pop('A+');
thresh_mrw.pop('D-');

ind_badges_mrw = [[exid,bt,bw,bc,1] for i,ex in enumerate(examples_mrw) for bc,(bt,bw) in zip(ex,weights_mrw.items()) 
                                      for exid in bc*[i]]
per_badge_df_mrw = pd.DataFrame(ind_badges_mrw,columns=['example','badge','complexity','count','weight'])

# weight community badges, 
community_weights = {'plus': 3*weights_mrw['practice']/10,'experience_makeup':weights_mrw['experience']/3,
                    'review_makeup':weights_mrw['review']/4,
                     'review_upgrade': (weights_mrw['practice']-weights_mrw['review'])/3,
                    'practice_makeup':weights_mrw['practice']/7}

learning_df = pd.Series(weights_mrw,name ='complexity').reset_index()
learning_df['badge_type'] = 'learning'
comm_df  = pd.Series(community_weights,name='weight').reset_index()
comm_df['badge_type'] = 'community'
# nans are for learning badges which all ahve weight 1
influence_df = pd.concat([learning_df,comm_df]).fillna(1).rename(columns={'index':'badge'})
# final df
influence_df['influence'] = influence_df['complexity']*influence_df['weight']
```

Grade cutoffs for total influence are:

```{code-cell} ipython3
:tags: [hide-input]

th_list = [[k,v] for k,v in thresh_mrw.items()]
pd.DataFrame(th_list, columns = ['letter','threshold']).sort_values(by='threshold').set_index('letter')
```

The total influence of each badge is as follows:

```{code-cell} ipython3
:tags: [hide-input]

# display
influence_df[['badge_type','badge','complexity','weight','influence']]
```

```{code-cell} ipython3
:tags: [hide-input]

# example calculation helper functions
def commumunity_example(badges,exid,cw_type):
    case_weights = weights_mrw.copy()
    case_weights['community'] = community_weights[cw_type]
    return [[exid,bt,bw,bc] for bc,(bt,bw) in zip(badges,case_weights.items()) 
                                      for i in range(bc)]

def commumunity_example(badges,exid,cw_type):
    case_weights = weights_mrw.copy()
    if type(cw_type)==list:
        for cw in cw_type:
            case_weights['community_'+cw] = community_weights[cw]
    else:
        case_weights['community'] = community_weights[cw_type]
#     print(badge)
    return [[exid,bt,bt.split('_')[0],bw,bc] for bc,(bt,bw) in zip(badges,case_weights.items()) 
                                      for i in range(bc)]
# 


def get_row(exid,badge_detail,badge_category,badge_mult,badge_count):
    if 'community' in badge_detail:
        badge_complexity = 1
        badge_weight = badge_mult
    else: 
        badge_complexity = badge_mult
        badge_weight = 1
    
    badge_row = [exid,badge_detail,badge_category,
                 badge_complexity, badge_weight,badge_count]
    return badge_row

def commumunity_example_comp_w(badges,exid,cw_type):
    case_weights = weights_mrw.copy()
    if type(cw_type)==list:
        for cw in cw_type:
            case_weights['community_'+cw] = community_weights[cw]
    else:
        case_weights['community'] = community_weights[cw_type]
#     print(badge)
    return [get_row(exid,bt,bt.split('_')[0],bw,bc) for bc,(bt,bw) in zip(badges,case_weights.items()) 
                                      for i in range(bc)]
# make more examples
ind_badges_mrw_c = [get_row(str(exid),bt,bt,bw,bc) for i,ex in enumerate(examples_mrw) for bc,(bt,bw) in zip(ex,weights_mrw.items()) 
                                      for exid in bc*[i]]

examples_mrw_cplus = [[24,0,0,0,0,10],[24,18,0,0,0,10],[24,0,18,0,0,10],[24,12,12,0,0,10],
                     [24,0,18,0,1,10],[24,12,12,2,0,10]]
ind_badges_mrw_c +=[r for i,ex in enumerate(examples_mrw_cplus) 
                    for r in commumunity_example_comp_w(ex,str(i)+'cp',['plus'])]
examples_mrw_em = [[22,0,0,0,0,6],[21,18,0,0,0,9],[23,0,18,0,0,13],[20,12,12,0,0,12],[20,12,12,0,0,12]]
ind_badges_mrw_c +=[r for i,ex in enumerate(examples_mrw_em) 
                    for r in commumunity_example_comp_w(ex,str(i)+'cem',['experience_makeup'])]
examples_mrw_rm = [[22,17,0,0,0,6,4],[24,10,12,0,0,0,8]]
ind_badges_mrw_c +=[r for i,ex in enumerate(examples_mrw_rm) for r in 
                    commumunity_example_comp_w(ex,str(i)+'cemrm',['experience_makeup','review_makeup'])]
examples_mrw_ru = [[24,0,16,0,0,0,0,14],[23,1,16,0,0,3,3,7]]
ind_badges_mrw_c +=[r for i,ex in enumerate(examples_mrw_ru) for r in 
                    commumunity_example_comp_w(ex,str(i)+'cemrupm',['experience_makeup','review_upgrade','practice_makeup'])]
# ind_badges_mrw_c

per_badge_df_mrw_c = pd.DataFrame(ind_badges_mrw_c,columns=['example','badge_det','badge',
                                                            'complexity','weight','count'])
per_badge_df_mrw_c['influence'] = per_badge_df_mrw_c['complexity']*per_badge_df_mrw_c['weight']

# get example letter grades
grade_calc = lambda df: (np.floor((df.sum()-48)/(delta/3))*(delta/3)+48).astype(int)
ex_grade = per_badge_df_mrw_c.groupby(['example'])['influence'].apply(grade_calc).reset_index().rename(
                    columns = {'influence':'influence_total'})

# get letter for each example
thresh_mrw_rv = {v:k for k, v in thresh_mrw.items()}
thresh_mrw_rv[0] = 'F'
thresh_mrw_cutoffs = np.asarray(sorted(thresh_mrw_rv))
ex_grade['letter'] = ex_grade['influence_total'].apply(lambda v: thresh_mrw_rv[thresh_mrw_cutoffs[(v > thresh_mrw_cutoffs)].max()])

# improve sample names
example_names = {old:'example ' +str(i) for i,old in enumerate(list(ex_grade['example']))}
ex_grade['example'] = ex_grade['example'].replace(example_names)
per_badge_df_mrw_c['example'] = per_badge_df_mrw_c['example'].replace(example_names)
# ex_grade = ((per_badge_df_mrw_c.groupby(['example'])['influence'].sum()-48).floordiv((delta/3))*(delta/3)+48).astype(int).reset_index()


per_badge_df_mrw_cletter = pd.merge(per_badge_df_mrw_c,ex_grade[['example','letter','influence_total']],on='example')

# sort to improve visual display
badges_in_order = ['experience','community_experience_makeup', 'review',
                   'community_review_makeup','community_review_upgrade',
                  'practice','community_practice_makeup', 'explore', 'build','community_plus']
badge_order_num ={b:i for i,b in enumerate(badges_in_order)}
per_badge_df_mrw_cletter['badge_num'] = per_badge_df_mrw_cletter['badge_det'].apply(lambda bd:badge_order_num[bd])

# per_badge_df_mrw_c= per_badge_df_mrw_c.sort_values(by='example')
per_badge_df_mrw_cletter = per_badge_df_mrw_cletter.sort_values(by=['badge_num','influence_total'],ascending=True,)
```

```{code-cell} ipython3
:tags: [hide-input]

# make plot
fig_cur = px.bar(per_badge_df_mrw_cletter,x='example',y='influence',color='badge_det',
                 hover_data=['badge','count','letter'],height=700)
fig_cur.update_layout(yaxis = dict(tickmode='array',
                              tickvals = list(thresh_mrw.values()),
                              ticktext =list(thresh_mrw.keys()),
                                  title='grade'))
# fig.update_layout( xaxis={'categoryorder':'array','categoryarray':per_badge_df_mrw_cletter['influence_total'].unique()})
fig_cur
```

```{important}
the labels on the horizontal axis are just example names, they do not have any meaning, I just have not figured out what I want to replace them with that might have meaning and need some sort of unique identifier there for the plot to work. 
```

+++

```{warning}
Officially what is on the [](grading) page is what applies if this page is in conflict with that.  
```

The total influence of a badge on your grade is the product of the badge's weight and its complexity.  All learning badges have a weight of 1, but have varying complexity.  All community badges have a complexity of 1, but the weight of a community badge can vary depending on what learning badges you earn. 

There are also bonuses: 
```{list-table}

*   - Name
    - Definition
    - Influence
*   - Early bird
    - 6 review + practice submitted by 2/15 
    -
*   - Participation
    - 22 experience badges
    -
*   - Lab
    - 13 lab badges
    -
*   - Breadth
    - If review + practice badges >-18:
    -
*   - Git-ing unstuck 
    - fix mistakes using git effectively
    - 
*   - Descriptive commits
    - all commits in KWL repo and build repos after penalty free zone have descriptive commit messages
    - 
```

```{note}
These bonuses are not pro-rated, you must fulfill the whole requirement to get the bonus.
```

```{important}
the grade plans on the grading page includes earning the Participation, Lab, and Breadth bonuses
```

If you are missing learning badges required to get to a bonus, your community badges will fill in for those.  If you meet all of the thresholds, the community badges will be applied with more weight to give you a step up (eg C to C+ or B+ to A-). 

Community badges have the most weight if you are on track for a grade between D and B+  

If you are on track for an A, community badges can be used to fill in for learning badges, so for example, at the end of the semester, you might be able to skip some the low complexity learning badges (experience, review, practice) and focus on your high complexity ones to ensure you get an A. 

More precisely the order of application for community badges: 
- to make up missing experience badges 
- to make up for missing review or practice badge to reach a total of 18 between these two types
- to upgrade review to practice to meet a threshold
- to give a step up (highest weight)
