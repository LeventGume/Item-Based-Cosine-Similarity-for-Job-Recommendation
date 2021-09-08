# Item-Based-Cosine-Similarity-for-Job-Recommendation

![photo](https://miro.medium.com/max/1200/1*rTZvrFD258ZZwvGy7nyqDw.jpeg)

This is a rating based approach to an implicit job recommendation competition that is arranged by Techcareer.net and launched on kaggle.

You can reach the dataset used in this project by [Kaggle link](https://www.kaggle.com/c/datathon-guess-the-last-one) of the competition.

## Problem Description
The aim of this competition is finding the top 10 best fitting jobs for all the job seekers in our dataset. 

## Datasets
**data_aday_log** : The main dataset provided by the company includes all the job applications of the job seekers who applied for a job in the first 15 days of the 2021. 

Columns: *jobseekerId*, *jobId*, *applicationDate*

---
**data_cv_details** : Dataset that contains jobseeker information.

Columns:*jobseekerId*,	*jobseekerCity*,	*jobseekerLastPosition*,	*departmentName*,	*totalExperienceYear*

_Note : "Other" value in the jobseekerCity column means the jobseeker lives in a different country or he/she did not want to share location information._

_Note2 : totalExperienceYear is the sum of all experiences of jobseeker that is written on the cv . 0 means the jobseeker has less than 12 month of experience._

---
**data_job_details** : Dataset that contains job information.

Columns: *jobId*,	*jobPosition*,	*jobDescription*,	*jobCity*,	*minExperience*,	*maxExperience*

_Note : minExperience - maxExperience columns:_

- _5 - 0 : min 5 years experience._
- _0 - 5 : max 5 years experience._
- _99 - 99 : experience is not important._
- _98 - 98 : inexperienced applicants._

## Evaluation Metric

Evaluation metric used in this competition is  Normalized Discounted Cumulative Gain (NDCG) assumed k=10 (10 jobs result list).

Discounted Cumulative Gain is a  measure of ranking quality. DCG measures the usefulness of the recommended job based on its position in the result list. The gain is accumulated from the top of the result list to the bottom, with the gain of each result discounted at lower ranks.

[For more information about DCG and NDCG]( https://en.wikipedia.org/wiki/Discounted_cumulative_gain)

## Approach used in this Project
