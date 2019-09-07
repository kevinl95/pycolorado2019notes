# Optimizing SQL + Python Pipelines for Data Science
## Jordan Hagan, Miner & Kasch
---
### Why am I giving this talk
- Kaggle Competitions and Data Science tutorials provide relatively clean CSVs that give the illusion of ease
- Real world data is messy and lives in databases, like SQL databases

### SQL Best Practices

FROM statement determines how you will structure the rest of your query. You will want your FROM table to be a core table with the fewest columns and rows that is highly indexed. USERS versus ORDERS for example depending on what you actually need.

Temp tables keep your code readable and makes it easier to troubleshoot. Single responsibility principle. The query optimizer may not be able to poperly optimize a query with subqueries and will likely result in longer run times.

Union All is faster than Union Distinct

Don't pull in columns you don't need

Use your indices as much as possible

### Joining Multiple Data Sources

SQL was designed for this

Even if you have mulitple data raw data files, standing up a quick database and loading the CSVs in there is better than bringing them right into Pandas. You don't want to have to reload the file every time you want to look at the data.

More data isn't always better, does not necessarily lead to better machine learning scores. Time frame considerations- do you see a dramatic improvement in model scores with two years of data versus one? If don't, do not pull in two years of data.

### Learning Curves to Help Determine Dataset Size

Learning curves help you understand not only your algorithm's bias vs. variance but also how many records you need to train a model you're happy with.

If high varience, more data will help. Otherwise it may make things worse.

### Feature Engineering
A lot of features can be created before you even load the data if you'd like.

Lead, Lag, and Rank can be much faster in SQL than Pandas.

### Optimizing Reading and Writing
Panda Read SQL and Read_GBQ() are natoriously slow. The best way to do this is to save your final query as a table and exprot that table to a CSV, then load the CSV into pandas via read_csv(). What this also allows is then for each time going forward you only have to load the CSV directly.

Writing to SQL is also slow. SQLAlchemy and Pandas, use bulk writing it is much faster.

### Conclusion
- SQL is incredibly powerful
- Knowing what tool is right for the job is incredibly powerful.

### Question Responses
Standardizing/Cleaning data is best done in code, like Python. More tools available.

Maximum dataset size where you recommend Pandas vs. SQL: very subjective, depends on what's in the db (like lots of strings instead of numbers). Both rows and volumns take up a lot of space. 

NaN values are subjective- can be dropped, but sometimes rows with NaNs offer better predictive power. Can also randomly drop sparse data, keeping some with some random threshold.