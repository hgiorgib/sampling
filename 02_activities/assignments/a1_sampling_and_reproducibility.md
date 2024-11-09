# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Henry Giorgi

```
1. Identify all stages at which sampling is occurring in the model.

* Initial Infection Sampling: The model first simulates infections across event types (weddings and brunches). Each individual has a 10% chance of infection (a Bernoulli distribution with p = 0.1). This phase determines the true cases based on event attendance.

* Primary Contact Tracing Sampling: After infections are determined, each case has a 20% chance of being traced, representing the limited tracing capacity often seen in real-world contact tracing. This introduces a non-random sampling bias since the sample may not reflect the true spread across all events.

* Secondary Contact Tracing Sampling: If multiple cases from the same event are detected independently, a “secondary” tracing step occurs where all attendees of the event are traced. This step overrepresents larger events (weddings), which aligns with Whitby’s observation that structured events are easier to trace.


2. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

* Sampling Procedure:
The simulation generates infections using a Bernoulli distribution with a probability based on an assumed infection rate. Infected individuals are traced with a 20% probability in the primary tracing phase. If multiple infections link to a single event, secondary tracing assumes a 100% success rate in detecting all infections at that event.

* Sample Size:
The initial infection sample includes all attendees (1,000 people). The traced sample then depends on the success rate of contact tracing (20% probability) and the secondary tracing mechanism for events with multiple cases. 

* Sampling Frame: 
The script simulates a population of 1,000 people who attend different types of gatherings: two large events (weddings) and 80 smaller events (brunches). Each person attends only one event, forming the sampling frame of the study. This setup reflects the blog post's example, where structured, larger events (e.g., weddings) contrast with smaller gatherings (e.g., brunches), which are more challenging to trace accurately


3. Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

* When running whitby_covid_tracing.py, the results resemble the distributions in Whitby’s blog post. The graphs show an overestimation of cases linked to large events due to biased secondary contact tracing. 


4. Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

* Reducing the number of repetitions from 50,000 to 1,000 introduces more variability in results, as seen in the provided simulations for 1,000 repetitions. With fewer samples, individual runs may display greater variance, making the results less stable and less reflective of the overall trend. This illustrates the Law of Large Numbers, where increasing sample size generally improves the reliability of statistical estimates​


5. Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times.

* By adding a fixed random seed in the scrip, it is possible to ensure reproducibility: np.random.seed(42). This addition controls the randomness in sampling by ensuring consistent outcomes across runs, regardless of random operations in the code. While the output may differ from Whitby’s post due to different assumptions or settings, setting a seed confirms that observed variability is due to model parameters and not random fluctuations​

```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `sampling-and-reproducibility`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
