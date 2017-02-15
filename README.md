#A/B Testing for Introducing a Screener

##Experiment Design
###Metric Choice

**List which metrics you will use as invariant metrics and evaluation metrics here.**  

Invariant Metrics : Number of clicks, Number of cookies, Click-through-probability  
Evaluation metrics : Gross conversion, Retention, Net conversion

**For each metric, explain both why you did or did not use it as an invariant metric and why you did or did not use it as an evaluation metric. Also, state what results you will look for in your evaluation metrics in order to launch the experiment.**

1. Number of cookies: Good invariant metric. Number of cookies will not change in the course of experiment.
2. Number of user-ids: The user-ids will not be available unless users register for free trial. Hence, it is not a good invariant metric. User-ids can be used as are evaluation metric as there might be a difference between number of visitors in the experiment and control groups. But this metric is not normalised. Hence, this is not ideal metric for both invariant and evaluation metric.
3. Number of clicks: Good invariant metric. Number of clicks will not change in the course of experiment.
4. Click-through-probability: This one is a good invariant metric because the clicks happen before the user sees the experiment.  
5. Gross conversion: This cannot be an invariant metric because the conversion can vary for the experiment and control group. On the other hand, this is a very good evaluation metric. The gross conversion can be different in both control and experiment group hence can be used as an evaluation metric.
6. Retention: This is the ratio of number of users who remain after 14 day trial and make first payment to the number of users who sign up for 14 days trial.This is not a good invariant metric because the number of users who enroll in the free trial is dependent on the experiment. This is a very good evaluation metric because the retention ratio in experiment group is expected to be higher because of low enrolment , if experiment meets the assumption.  
7. Net conversion: Again, this is not a good invariant metric because the number of users who enroll in the free trial is dependent on the experiment. Net conversion would be higher/lower for the experiment group depending on the outcome of the experiment. This will be a good evaluation metric as it is directly dependent on the effect of the experiment.

For the sake of this project, I will focus on Gross Conversion and Net conversion Metrics. Gross conversion metric will imply if we lower our costs by introducing the screener pop-up. The net conversion metric will show us how the change affects our revenues.Hence, for effectiveness of the experiment, we should expect to observe decrease in Gross Conversion metric and no decrease in Net Conversion Metric.

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
From the number of pageviews quiz, I made the following calculation for the two metrics : 

| Metric        | Value   | Standard Deviation  | Pageviews   |
| ------------- |:-------------:| -----:| ---------:|
| Gross Conversion      | 0.2063 | 0.0202 | 645875 |
| Net Conversion      | 0.1093 | 0.0156  | 685325 |

It would not make sense to use Bonferroni correction as we are using just two metrics which are highly correlated. During this experiment, there is no chance that anyone would get hurt. Also, there is no sensitive data. Hence, it would be fine to divert the entire traffic towards this experiment.

####Duration vs. Exposure
**Indicate what fraction of traffic you would divert to this experiment and, given this, how many days you would need to run the experiment.**

I would divert 70% of the traffic to the experiment. Given that, the experiment will take 25 days, which is a reasonable time for our needs.

**Give your reasoning for the fraction you chose to divert. How risky do you think this experiment would be for Udacity?**

The experiment is not extremely risky given that it does not affect existing paying customers, and is simple enough that there is a low chance of bugs occurring in the process. Nevertheless it may have a substantial impact on new enrollments, and diverting 100% of the traffic may thus not be advisable.

## Experiment Analysis
### Sanity Checks
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

### Result Analysis
#### Effect Size Tests
**For each of your evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant.**

```
Gross Conversion : [-0.0291, -0.0120] 
Statistically Significant : YES
Practically Significant : YES

Net Conversion: [-0.0116, 0.0019]
Statistically Significant : NO
Practically Significant : NO
```

#### Sign Tests
**For each of your evaluation metrics, do a sign test using the day-by-day data, and report the p-value of the sign test and whether the result is statistically significant.**

```
Gross conversion: 0.0026
Statistically Significant : YES

Net Conversion: 0.6776
Statistically Significant : NO
```

### Summary
**State whether you used the Bonferroni correction, and explain why or why not. If there are any discrepancies between the effect size hypothesis tests and the sign tests, describe the discrepancy and why you think it arose.**

I did not use Bonferroni correction. This is because, using it will make the experiment more conservative. The Bonferroni correction is designed to be used with multiple metrics. In this experiment, we have multiple metrics and we need all of them to meet some criteria in order to launch. If we had multiple metrics, but we would need only one of them to meet our criteria in order to launch, then the Bonferroni correction would have been useful. But we need multiple metrics to be satisfied. Hence, it would not be useful to use Bonferroni correction here. Bonferroni correction is designed for another type of errors, for example, it can help us if planned to launch experiment if one or another metric became statistically significant.There was no discrepancy between the hypothesis test and sign test.  


### Recommendation
**Make a recommendation and briefly describe your reasoning.**  
I performed two hypothesis test. First Gross Conversion and second Net Conversion.

The Gross Conversion is defined as the ratio of the number of users enrolling in the course to the number of user who clicked Start Now Button. As the experiment page recommends the time required per week to complete this course, it will reduce the total number of users enrolling for free Trial. Also the coaches will be able to concentrate on less number of students and able to convert them to paid users. 

The Net Conversion is defined as the number of users who enrolled for the Free Trial and make their first payment to the number of users who clicked the start free trial button.

I would recommend that the Gross Conversion Metric is actually showing positive results. The students who left are those who do not have enough time for courses. In Net Conversion Metric, I do not see statistically significant change. But,the confidence interval includes the negative of the practical significance boundary. There is possibility that the number went down to an amount that matter to bussiness. To recommend, I would not support launching the project.

### Follow-Up Experiment
**Give a high-level description of the follow up experiment you would run, what your hypothesis would be, what metrics you would want to measure, what your unit of diversion would be, and your reasoning for these choices.**  

I would like to put a follow up experiment in which the student needs to do a free quick course whose score would recommend the student if he/she is ready to take it or not. This will make sure all the students pay before they join the course. This will also efficiently utilize coaches' time.

In order to reduce the attrition rate in early of course, that is those students who left the course early because they are unknowledgeable about pre requisite leanings. We need a course or a Project, such that the users able to get an idea what prerequisite knowledge they should know & and what the course is all about. The system also need an auto grader so coaches would spend more time to help those users who passed this project and continued in the Course in Paid service.

The hypothesis is that Udacity will be able reduce the number of frustrated students that leave courses mid-way thereby getting a negative feeling about Udacity and also wasting coaches' time. The unit of diversion would be user ids when they register for introductory course.

Invariant Metrics: Number of users enroll in introductory free course.

Evaluation Metrics: 
Net Conversion : The net conversion would remain low as the number of students who pass the introductory course would be less and lesser will be the students who actually pay for further courses.

Course Graduate Ratio: The Course Graduate Ratio are those users who completed the paid courses divided by total users who paid there first payment. The purpose for this metric is to predict the introductory course affected the Completion Ratio is positive or in negative way. This Metric maybe remain high, as only those student able to get in paid service who are really interested in passing the course.
