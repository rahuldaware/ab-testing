#A/B Testing for Introducing a Screener

##Experiment Design
###Metric Choice

**List which metrics you will use as invariant metrics and evaluation metrics here.**  

Invariant Metrics : Number of clicks, Number of cookies, Click-through-probability  
Evaluation metrics : Gross conversion, Retention, Net conversion

**For each metric, explain both why you did or did not use it as an invariant metric and why you did or did not use it as an evaluation metric. Also, state what results you will look for in your evaluation metrics in order to launch the experiment.**

1. Number of cookies: Good invariant metric. Number of cookies will not change in the course of experiment.
2. Number of user-ids: The user-ids will not be available unless users register for free trial. Hence, it is not a good invariant metric. User-ids are not good evaluation metric because there might be a difference between number of visitors in the experiment and control groups. Hence, this is not ideal metric for both invariant and evaluation metric.
3. Number of clicks: Good invariant metric. Number of clicks will not change in the course of experiment.
4. Click-through-probability: This one is a good invariant metric because the clicks happen before the user sees the experiment.  
5. Gross conversion: This cannot be an invariant metric because the conversion can vary for the experiment and control group. On the other hand, this is a very good evaluation metric. The gross conversion can be different in both control and experiment group hence can be used as an evaluation metric.
6. Retention: This is the ratio of number of users who remain after 14 day trial and make first payment to the number of users who sign up for 14 days trial.This is not a good invariant metric because the number of users who enroll in the free trial is dependent on the experiment. This is a very good evaluation metric because the retention ratio in experiment group is expected to be higher because of low enrolment , if experiment meets the assumption.  
7. Net conversion: Again, this is not a good invariant metric because the number of users who enroll in the free trial is dependent on the experiment. Net conversion would be higher/lower for the experiment group depending on the outcome of the experiment. This will be a good evaluation metric as it is directly dependent on the effect of the experiment.

For the sake of this project, I will focus on Gross Conversion and Net conversion Metrics. Gross conversion metric will imply if we lower our costs by introducing the screener pop-up. The net conversion metric will show us how the change affects our revenues.Hence, for effectiveness of the experiment, we should expect to observe decrease in Gross Conversion metric and increase in Net Conversion Metric.

###Measuring Standard Deviation
**List the standard deviation of each of your evaluation metrics**
The standard deviation is calculated with the formula : SD = sqrt((p*(1-p)/N)
```
Net Conversion: N=400; p=0.1093; SD=0.0156
Gross Conversion: N=400; p=0.2063; SD=0.0202
```

**For each of your evaluation metrics, indicate whether you think the analytic estimate would be comparable to the the empirical variability, or whether you expect them to be different (in which case it might be worth doing an empirical estimate if there is time). Briefly give your reasoning in each case.**

Empirical Standard deviation should be comparable to analytic estimate for Gross and Net conversion because unit of diversion and unit of analysis is the same i.e. number of cookies.

###Sizing
####Number of Samples vs. Power
**Indicate whether you will use the Bonferroni correction during your analysis phase, and give the number of pageviews you will need to power you experiment appropriately**

I selected Gross Conversion and Net conversion as my evaluation metrics. I will need 685324 pageviews to power the experiment with these metrics. 

####Duration vs. Exposure
**Indicate what fraction of traffic you would divert to this experiment and, given this, how many days you would need to run the experiment.**

I would divert 70% of the traffic to the experiment. Given that, the experiment will take 25 days, which is a reasonable time for our needs.

**Give your reasoning for the fraction you chose to divert. How risky do you think this experiment would be for Udacity?**

The experiment is not extremely risky given that it does not affect existing paying customers, and is simple enough that there is a low chance of bugs occurring in the process. Nevertheless it may have a substantial impact on new enrollments, and diverting 100% of the traffic may thus not be advisable.

##Experiment Analysis
###Sanity Checks
**For each of your invariant metrics, give the 95% confidence interval for the value you expect to observe, the actual observed value, and whether the metric passes your sanity check.**

```
Number of cookies : [0.4988, 0.5012]
Observed : 0.5006
Result : PASS

Number of clicks on Start free trial : [0.4959, 0.5041]
Observed : 0.5005
Result : PASS

Click-through-probability on Start free trial : [0.0812, 0.0830]
Observed 0.0822
Result : PASS
```

###Result Analysis
####Effect Size Tests
**For each of your evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant.**

```
Gross Conversion : [-0.0291, -0.0120] 
Statistically Significant : YES
Practically Significant : YES

Net Conversion: [-0.0116, 0.0019]
Statistically Significant : NO
Practically Significant : NO
```

####Sign Tests
**For each of your evaluation metrics, do a sign test using the day-by-day data, and report the p-value of the sign test and whether the result is statistically significant.**

```
Gross conversion: 0.0026
Statistically Significant : YES

Net Conversion: 0.6776
Statistically Significant : NO
```

####Summary
**State whether you used the Bonferroni correction, and explain why or why not. If there are any discrepancies between the effect size hypothesis tests and the sign tests, describe the discrepancy and why you think it arose.**

I did not use a Bonferroni correction because we are only testing one variation. It might be useful to apply the Bonferroni correction if we decide to do post-test segmentation on the results, for example based on browser type or countries of origin.

###Recommendation
**Make a recommendation and briefly describe your reasoning.**

The metrics I was interested in were **Gross conversion** and **Net conversion**.

Gross conversion turned out to be negative and practically significant. This is a good outcome because we lower our costs by discouraging trial signups that are unlikely to convert.
Net conversion unfortunately ended up being statistically and practically insignificant and the confidence interval includes negative numbers. Therefore, there is a risk that the introduction of the trial screener may lead to a decrease in revenue.

We should therefore consider test other designs of the screener before we decide whether to release the feature, or abandon the idea entirely.

### Follow-Up Experiment
**Give a high-level description of the follow up experiment you would run, what your hypothesis would be, what metrics you would want to measure, what your unit of diversion would be, and your reasoning for these choices.**  

Goals of any company are earn money by satisfying customer needs. I this experiment we tried to reduce distraction of users, who are going to enroll to trial but not going to spend a lot on time by studying. But we can work with other group of students, who auditing course for free, but spend more than 5 hours a week. If they decide to switch to non-free service, they can improve quality of learning and receive valuable certificate. For the company it can increase the revenue.

So, the null hypothesis is: Showing of "start trial screen" for students who have access to course materials and spend more than 5 hours a week will not increase retention.

Because we want to introduce this feature to user already signed to our coursed unit of diversion should be user_id. As invariant metrics we can use number of active user_id's, because it's our unit of diversion and number of users clicking 'access course materials', because we measure it before the experiment stage.

As evaluation metric we can use overall retention, because we want to increase number of paying customers by this change.

### References
- http://www.utdallas.edu/~herve/Abdi-Bonferroni2007-pretty.pdf
- https://en.wikipedia.org/wiki/Standard_deviation
- http://graphpad.com/quickcalcs/binomial1.cfm
