# Item-Based-Cosine-Similarity-for-Job-Recommendation

![photo](https://miro.medium.com/max/1200/1*rTZvrFD258ZZwvGy7nyqDw.jpeg)

This is a rating based approach to an implicit job recommendation competition that is arranged by Techcareer.net launched on kaggle.

You can reach the dataset used in this project by [Kaggle link](https://www.kaggle.com/c/datathon-guess-the-last-one) of the competition.

## Problem Description
The aim of this competition is finding the top 10 most suitable jobs for all the job seekers in our dataset based on their past applications and the information provided about jobs and jobseekers. 

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

## Approach Used in This Project

Altough the problem on its nature has an implicit feedback system (no rating, no negative or positive feedback), i think how suitable is a job to a person can be measurable. By using them, it is possible to create a rating for each job application that shows how relevant that job for the jobseeker. There are several aspects that are present in our data that can help us to build a rating system:
- Job city can be same with the jobseekers city
- The experience needed for that particular job can be satisfied by the jobseeker
- The similarity of the job and the previous job of the jobseeker

```python
#Combining all ratings into one and distribution of the rating among the jobseekers
cv_job_merge['rating']=1+cv_job_merge.EnoughExp+cv_job_merge.city_control+cv_job_merge.jobPosition_rule
df=cv_job_merge[['jobId_x','jobseekerId','rating']]
df.rating.hist()
```
![image](https://user-images.githubusercontent.com/42347243/132832095-be0cb77a-3830-4214-a1ea-54f4d377ebf1.png)



With this rating based approach, for the simplicity purposes, a simple [item based collabrative filtering (by using cosine similarity)](https://en.wikipedia.org/wiki/Item-item_collaborative_filtering) is used as the model.


## How to Improve This Approach

Because of the time and resource limitation of the competition there were several approaches that we could not find a chance to try.
Here is a short list for future improvements:
- A more detailed item based similarity by using job description provided in the job details dataset.
- User based similarity approach (out of memory (RAM) on kaggle)
- A more complex recommendation system algorithms can be used. (mixed collabrative filtering and content based models etc) 
- Ratings can be improved 
  * Last position of jobseeker and the job detail can be matched based on the similarity
  * To match jobseeker city and job city, the latitude and logitude based Euclidean distance can be used.
  * For all of these aspects, the tendency of the jobseeker can be found. (For instance, how important the job location (or distance) for the jobseeker based on their past applications?). Ratings can be recalculated by using these tendency scores.

   
