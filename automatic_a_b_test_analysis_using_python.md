# Stats Don't Have to Be Scary: Automatic a/b Test Analysis Using Python
## Kristie Wirth, Data Scientist at Zapier
[Slides](www.bit.ly/2lXuHdN)
---

### Why do I need to do A/B testing?
Testing new features on users live to see if it works. A group sees the feature, B group does not for example. Let's you roll back potentially damaging changes without hurting all the users, or you can then roll it out to everyone if the A group likes the change.

"Installing this feature should lead to a 5-10% upgrade rate" <-- Let's you say things like this with data.

### Assigning Groups
Need a 'treatment' and a 'control' bucket.

50-50? Might be too risky. Maybe 30-70 or 10-90. 

Don't want a mismatched jarring experience. Users need to consistently see/not see the new feature.

Also need to make sure you don't keep putting the same users in the 'treatment' bucket or it becomes too hard to determine what feature influenced their decisions.

### Analysis

You have a birth event (assigning the user to the treatment or control group) and the death event (when someone signs up, upgrades, uses the new thing, etc.). The death event is when they exit the study.
Also need a timeframe to convert the user. If they don't convert, they exit the study.
Exclusions- exclude people from your study that shoulnd't count, like employees in your org or spam users.
Now you can use SQL etc. to collect data about conversion rate, timeframe, etc.

### Uncertainty

This test was at a certain point in time, with a certain group of people.
How can you predict what you'll actually see in production?
You need your control distribution, treatment distribution, take their difference, compute an upper and lower bound on your uncertainty, and compute your error in your conversion rate so you can say what your expected conversion rate is plus or minus something.

### Web App

Speaker built a web app that:
- Generates code for the AB test based on a hypothesis and thresholds for creating groups
- Creates analytics based on the conversion event, goal, timeframe, etc.
- Generates an analysis of the experiment as a report that lets you determine whether to install. Even has a bottom line recommendation

Resources in the linked slides (above) has code for the condtion assignment, conversion rate SQL, bayesian analysis code, and the Redshift database-> Python code generator.