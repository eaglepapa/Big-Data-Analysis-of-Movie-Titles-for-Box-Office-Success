# Big Data Analysis of Movie Titles for Box Office Success

## Table of Contents
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning/Preparation](#data-cleaningpreparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results/Findings](#resultsfindings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
- [References](#references)
- [Contact](#contact)

  
### Project Overview
---
This project uses data analysis and visualization to provide solution to eight business questions. Data analysis tools such as SQLiteStudio, Pandas, Pyspark, MongoDB, AWS Anthena, AWS S3, AWS Glue, were implemented in this project. Eight business questions were generated to solve the business problem. Five datasets were collected. The datasets contains data from 2026 to 1888. To focus on recent trends, the last five years data, thus data from 2024 to 2020 were focused on considering the business questions.

![Capture21](https://github.com/user-attachments/assets/ea901153-aceb-40f4-9644-648ff45b642c)


### Data Sources
Movie Data: The dataset was provided as part of ongoing studies

![Capture1](https://github.com/user-attachments/assets/9537a977-f498-452e-8b7c-8761b5d28713)


### Tools
- SQLiteStudio – It was used to perform SQL queries to merge multiple datasets depending on the business questions.
  [Download here](https://www.sqlitestudio.pl/)

- Pandas – It was used to perform Exploratory Data Analysis (EDA) to better understand the merged dataset.
  [Download here](https://pandas.pydata.org/)

- Pyspark – It was used to perform big data analysis.
  [Download here](https://spark.apache.org/docs/latest/api/python/

- MongoDB – It was used to query json file.
  [Download here](https://www.mongodb.com/)

- AWS – AWS anthena was implemented to create a schema for the AWS Glue database. A csv file was imported into AWS S3 bucket for analysis.
[Download here](https://aws.amazon.com/)

- Google Colab – It was used in this project for its free cloud computing, Python support and ease of access to libraries without the need for local installation.
[Download here](https://colab.research.google.com/)

#### Data Cleaning/Preparation
In the initial data preparation please, I performed the following tasks:
1.	Data loading and inspection.
2.	Performing SQL queries to merge tables
3.	Handling missing values.
4.	Data cleaning and formatting.
5. 	Building the model
5.	Predicting values

   
### Exploratory Data Analysis
EDA involved exploring the movie data to answer key questions, such as: 
1.	What is the top 10 trending primary titles in 2024 to 2020 each year using number of votes as a bench mark?
2.	What is the total number of primary titles that were voted for compared to primary titles that did not receive any votes from 2024 to 2020 each year?
3.	What are the different title types and their total number of primary titles each contains from 2024 to 2020 each year?
4.	What is the top five (5) genres in 2024 to 2020 each year using their average votes?
5.	What is the trend of the following genres, thriller, animation, adventure, mystery, music, using their average votes from 2020 to 2024?
6.	What are the first 5 primary titles in animation genre from 2024 to 2020?
7.	What are the first 5 primary titles in 2020 using number of votes?
8.	What are the total number of primary titles that had an average rate of five or more from 2024 to 2020 each years?

  
### Data Analysis 
```sql
CREATE TABLE movies2 AS
SELECT basics.tconst, basics.primaryTitle, basics.titleType, basics.startYear, basics.genres, ratings.numVotes, ratings.averageRating
FROM basics
FULL JOIN ratings ON basics.tconst = ratings.tconst
WHERE basics.startYear >= 2020 AND basics.startYear <= 2024
ORDER BY basics.startYear DESC, ratings.numVotes DESC;
```

```python
#Find correlation between number of votes and their average ratings
df24_corr = df24[['numvotes','averagerating']]
df24_corr.corr()
```

```javascript
db.movies.find({startyear: {$gte: 2020, $lte: 2024},genres:’animation’},
{_id:0,primarytitle:1,startyear:1}).sort({startyear:-1}).limit(5);
```

### Results/Findings
The analysis results are summarized as follows:
1. The top 10 trending primary titles in 2024 to 2020 each year using number of votes as a measure is clearly illustrated in the figures below;
   
![Capture37](https://github.com/user-attachments/assets/016bb45f-deec-49c5-8e87-7fcb31538d04)

![Capture40](https://github.com/user-attachments/assets/7da96305-97df-4212-ba01-1cc3c024363d)

![Capture44](https://github.com/user-attachments/assets/a6be80f6-b794-4177-865d-ea635e548909)

![Capture47](https://github.com/user-attachments/assets/f7d1ada9-14eb-4e27-9447-e3dcc035ae7a)

![Capture49](https://github.com/user-attachments/assets/05c20433-d4e6-4fba-bc38-803be268a4a4)



2. The total number of primary titles that were voted for compared to primary titles that did not receive any votes from 2024 to 2020 each year is clearly illustrated in the figures below;
   
![Capture52](https://github.com/user-attachments/assets/2ed120a1-7c14-4763-998d-f626b9b46298)

![Capture53](https://github.com/user-attachments/assets/10f48872-33d2-42cc-ae9c-475c578b45a9)

![Capture54](https://github.com/user-attachments/assets/7b655465-ab48-4eee-ae92-9cde54a66997)

![Capture55](https://github.com/user-attachments/assets/a9b4a329-f6cb-4568-94c5-1625b92e911c)

![Capture56](https://github.com/user-attachments/assets/a18aded0-60a9-4e0d-88c9-d945f0440580)



3.	The different title types and their total number of primary titles each contains from 2024 to 2020 each year is clearly illustrated in the figures below;
   
![Capture69](https://github.com/user-attachments/assets/e197a918-fcc7-44fc-a5c4-4f45e59799dc)

![Capture71](https://github.com/user-attachments/assets/b431d98d-bd3c-41b3-94e2-5e25f595cb07)

![Capture73](https://github.com/user-attachments/assets/ae6f8cc9-252b-43b8-941b-a9e55f29dd79)

![Capture75](https://github.com/user-attachments/assets/67876f34-04a6-4acc-9706-300fbe3320ab)

![Capture77](https://github.com/user-attachments/assets/9f491e1d-dda2-44dd-aca0-b96f518597d8)


   
4.	The top five (5) genres in 2024 to 2020 each year using their average votes is clearly illustrated in the figures below;

![Capture9](https://github.com/user-attachments/assets/d3615a82-f76c-4731-aa78-9c30a3abe638)

![Capture10](https://github.com/user-attachments/assets/97f3460a-0092-4468-b9ca-93b5c16c565f)

![Capture11](https://github.com/user-attachments/assets/2f963eae-e127-4b7f-bd6b-42420001a1bd)

![Capture12](https://github.com/user-attachments/assets/53ccf874-4a25-4f36-8bb8-3c898038eef8)

![Capture13](https://github.com/user-attachments/assets/161679f8-802a-445c-899e-c9c29e98d2fe)



5.	The trend of the following genres, thriller, animation, adventure, mystery, music, using their average votes from 2020 to 2024 is clearly illustrated in the figure below;

![Capture15](https://github.com/user-attachments/assets/86be2111-035f-4fb6-8c76-362b2b6860e2)

![Capture18](https://github.com/user-attachments/assets/be3695f4-641f-4f53-93fd-2745a5adb530)

![Capture19](https://github.com/user-attachments/assets/8172ffb5-6636-45ae-b54c-baa00b1ec681)

![Capture20](https://github.com/user-attachments/assets/f8a37e63-7af2-456a-8afd-843dceab38d7)

![Capture21](https://github.com/user-attachments/assets/123113d9-996a-4b91-afa6-48d435e95dbb)



6.	The first 5 primary titles in animation genre from 2024 to 2020 is clearly illusttrated in the figure below;


![Capture22](https://github.com/user-attachments/assets/6b35ab48-5b7d-40b2-aa58-1ffe77d879ca)



7.	The first 5 primary titles in 2020 using number of votes is clearly illusttrated in the figure below;


![Capture24](https://github.com/user-attachments/assets/5f6ec2d9-d693-472c-85da-940ff6361d33)



8.	The total number of primary titles that had an average rate of five or more for the year was 26.

![Capture6](https://github.com/user-attachments/assets/26ff03ec-9ca7-4802-87fe-808961ff0e90)

### Recommendations
1. Funds should be allocated to low performing movies and not where it is already doing well.
2. Focus marketing spendings on movies which are not performing well.
3. Analyze the key factors contributing to the success of top-performing movies and apply those insights to improve the performance of lower-rated or less popular titles.

### Limitations
The dataset was provided as part of ongoing studies, so its authenticity cannot be fully guaranteed.

### References
1.	Bae, G. and Kim, H., 2019. The impact of movie titles on box office success. Journal of Business Research, 103, 100–109.
2.	Chen, Y. and Dai, Z., 2022. Mining of Movie Box Office and Movie Review Topics Using Social Network Big Data. Frontiers in Psychology [online], 13. Available from: https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2022.903380/full [Accessed 28 Dec 2024].
3.	Chugh, V., 2023. Python pandas tutorial: The ultimate guide for beginners [online]. Available from: https://www.datacamp.com/tutorial/pandas [Accessed 29 Dec 2024].
4.	Del Vecchio, M., Kharlamov, A., Parry, G. and Pogrebna, G., 2021. Improving productivity in Hollywood with data science: Using emotional arcs of movies to drive product and service innovation in entertainment industries. Journal of the Operational Research Society, 72 (5), 1110–1137.
5.	Franses, P. H., 2021. Modeling box office revenues of motion pictures✰. Technological Forecasting and Social Change, 169, 120812.
6.	Hotz, N., 2018. What is CRISP DM? [online]. Data Science PM. Available from: https://www.datascience-pm.com/crisp-dm-2/ [Accessed 28 Dec 2024].
7.	IBM, 2021. What Is MongoDB? | IBM [online]. Available from: https://www.ibm.com/think/topics/mongodb [Accessed 1 Jan 2025].
8.	Kumar, S. and Kumari, S., 2020. Getting Started with SQL Using SQLite Studio. [online]. Available from: https://www.opensourceforu.com/2020/12/getting-started-with-sql-using-sqlite-studio/ [Accessed 28 Dec 2024].
9.	McKenzie, J., 2023. The economics of movies (revisited): A survey of recent literature. Journal of Economic Surveys, 37 (2), 480–525.
10.	Ni, Y., Dong, F., Zou, M. and Li, W., 2022. Movie Box Office Prediction Based on Multi-Model Ensembles. Information, 13 (6), 299.

## Contact
Feel free to reach out!  
📧 Email: [oduroprince08@gmail.com](mailto:oduroprince08@gmail.com) &nbsp;|&nbsp; 🔗 LinkedIn: [linkedin.com/in/oduroprince24](https://linkedin.com/in/oduroprince24)


🚀
📊
📈
🧠

Thanks for visiting! 😄
