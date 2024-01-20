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




# Office Hours & Communication



```{code-cell}
:tags: ["remove-input"]

import pandas as pd
from IPython.display import display, Markdown, HTML
pd.set_option('display.max_colwidth', 0)
# df = pd.read_csv('../_data/communication.csv')

help_df = pd.read_csv('../_data/help_hours.csv')
```

## Announcements

Announcements will be made via GitHub Release. You can view them [online in the releases page](https://github.com/introcompsys/fall2023/releases) or you can get notifications by watching the repository, choosing "Releases" under custom [see GitHub docs for instructions with screenshots](https://docs.github.com/en/account-and-profile/managing-subscriptions-and-notifications-on-github/setting-up-notifications/configuring-notifications#configuring-your-watch-settings-for-an-individual-repository). You can choose GitHub only or e-mail notificaiton [from the notification settings page](https://github.com/settings/notifications)

```{warning}
For the first few classes they will be made by BrightSpace too, but that will stop
```


````{admonition} Sign up to watch
:class: community, dropdown

Watch the repo and then create a file called `community.md` in your kwl repo and add a link to this section, like: 
```
- [watched the repo as per announcements](https://introcompsys.github.io/spring2023/syllabus/communication.html#announcements) 
```
put this on a branch called `watch_community_badge` and title your PR "Community-Watch"
````

## Help Hours


```{code-cell}
:tags: ["remove-input"]

help_df.style.hide(axis="index")
``` 

Online office hours locations are linked on the [GitHub Organization Page](https://github.com/introcompsys)

```{important}
You can only see them if you are a "member" to join, use the "Whole Class Discussion" link in prismia. 
```

<!-- 
## Getting Help 

- E-mail the instructor and TAs: `cscsystools-help-group@uri.edu`
- Post an issue to the course website
-  -->

<!--
Online office hours locations are linked in the #help channel on slack
We have several different ways to communicate in this course. This section summarizes them -->

<!--
## To reach out, By usage

```{code-cell}
:tags: ["remove-input"]

df = df[['usage','platform','area','note']]
display(HTML(df.style.hide_index()._repr_html_()))
```

```{note}
e-mail is last because it's not collaborative; other platforms allow us (Proessor + TAs) to collaborate on who responds to things more easily.
```

## By Platform

```{code-cell}
:tags: ["remove-input"]

for platform, data in df.groupby('platform'):
    display(HTML('<h3> Use '+ platform + ' for </h3>'))
    display(HTML(data.drop(columns='platform').style.hide_index()._repr_html_()))

``` -->

## Tips

### For assignment help

- **send in advance, leave time for a response** I check e-mail/github a small number of times per day, during work hours, almost exclusively. You might see me post to this site, post to BrightSpace, or comment on your assignments outside of my normal working hours, but I will not reliably see emails that arrive during those hours. This means that it is important to start assignments early.

### Using issues

- use issues for content directly related to assignments.  If you push your code to the repository and then open an issue, I can see your code and your question at the same time and download it to run it if I need to debug it
- use issues for questions about this syllabus or class notes. At the top right there's a GitHub logo {fa}`github` that allows you to open a issue (for a question) or suggest an edit (eg if you think there's a tpo or you find an additional helpful resource related to something)


```{admonition} ... 
:class: anchor,dropdown

You can submit a pull request for the typo above, but be sure to check the pull request tab of the repo before submitting to see if it has already been submitted.
```

### For E-mail

- use e-mail for general inquiries or notifications
- Please include `[CSC392]`  in the subject line of your email along with the topic of your message. This is important, because your messages are important, but I also get a lot of e-mail. Consider these a cheat code to my inbox: I have setup a filter that will flag your e-mail if you include that in subject to ensure that I see it.

```{admonition} Should you e-mail your work? 
:class: anchor,dropdown

No, request a pull request review or make an issue if you are stuck
```
