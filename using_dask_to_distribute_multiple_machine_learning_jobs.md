# Using Dask to Distribute Machine Learning Jobs
## William Cox, Data Scientis at Grubhub
---

### Problem they are Solving
Assigning drivers to timeslots
Too few drivers and customers are unhappy because no deliveries
Too many drivers and drivers are unhappy because they only make base rate and Grubhub is paying idle drivers
Predict how many orders will happen for all regions so the appropriate schedule can be made

### Prediction Cycle
Pull in historic order data, weather, sports, train model for each region, predict orders N weeks into the future

### Parallelization
Long-term forecasting is a batch job (can take several hours to predict three weeks into the future)
Creating mutli-week predictions for hundreds of different regions, for many different models
Need a system to do this in parallel across many machines

### Dask
Pythonic, simple, local testing/distributed deployment, minimal changes to existing codebase
Needs heavy compute but not necessarily heavy data. Most of the data will fit comfortably in memory
Other contenders: Celery, Apache Spark

Python only and small footprint!

#### Use Cases
Large NumPy/Pandas/Lists analysis
Custom task scheduling

#### Local and Distributed
Can configure both local and distributed clusters for different use cases. Threading, number of workers, etc.
Distributed code looks the same as the local code

#### Distributed on YARN
Dask workers are started in YARN containers, letting you allocate compute/memory resources on a cluster
Files are distributed via HDFS
Dask works nicely with Hadoop to create and manage Dask workers
Lets you scale Dask to many computers on a network. Can also do Kubernetes, SSH, GCP, AWS...

### Big ML
SKLearn, XGBoost, TensorFlow integrations
dask_ml lib is what you should look at

### Takeaways
Forecasing now scales with number of computers in cluster. 50% savings also in single-node compute because of distribution.
For distributing work across comptuers, Dask is a good place to start investigating.
YARN complicates matters (unsure if Kubernetes would be much better)
Dask website has lots of good documentation
Dask maintainers are active on StackOverflow
Dask is a complex library with many different abilities.