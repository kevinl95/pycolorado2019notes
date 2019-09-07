# Unleashing the Eighth Plague: An Intro to Load Testing with Locust and Python
## Gabriel Boorse, @gnboorse
---

### What is load testing?
Evaluating the performance of your website at scale. How many concurrent users can I have? What quality of service at load?

Inside the testing pipeline (Unit testing->Integration testing->UI Testing->Acceptance testing) it fits at any stage of the process. You may want to evaluate performance during every type of test.

We are looking for throughput, latency, and breaking points at various levels of load. 

Secret of effective load testing: you don't want these tests to pass. You're always trying to find the limit of the code you have. Design load tests that fail.

### Locust
FOSS library for load testing.
[Link to project webpage](http://locust.io)
Scalable user load testing tool written in Python
Decorators like @task for different endpoints where a client will repeatedly hit that endpoint.
Has a web UI that lets you see the load test as it occurs
Can run without web UI headlessly as well. Point it at your QA site. -c lets you set the number of users to spawn. -r is the rate to spawn them. They will execute each task you flagged with a decorator. 
Can pass parameters to task decorators to give them weights. Simulate a randomization of requests to a site where certain endpoints are hit more.
self.client in locust is really a wrapper around the popular requests library.
Can create sequential tasks with @seq_task(x) where x is the step number indexed at 1.
Can check if a failure occurs as a 'pass condition'. For example, testing if users get a 404 error. Could be good for security/permissions testing.

### Getting value from load test results
Measure everything
Search for bottlenecks
Monitor the system under test

### Taking Action
Fix the code <-- Best case
Scale up hardware resources
Decide to live with your findings :(

### Advanced Topics
#### Running Locust Distributed
Have a single controller talking with multiple agents that all load test the system you are trying to break. Can then spin up multiple VMs that communicate and test your system.
#### Testing non-RESTful Services
Sometimes your systems do not expose HTTP endpoints. There are APis for things like database queries, fire custom requests like sending a message on a message queue, etc.
