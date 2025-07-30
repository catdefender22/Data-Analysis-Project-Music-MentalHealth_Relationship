# Data Analysis Project 2 - How music influences our Mental health


![Microsoft SQL Server](https://img.shields.io/badge/Microsoft%20SQL%20Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=postgresql&logoColor=white)


## 📚 Table of Contents

- [Overview](#-overview)
- [Tools Used](#tools-used)
- [Dataset](#dataset)
- [Database](#database)
- [Data Processing](#data-processing)
- [Project Includes](#project-includes)
- [Conclusions](#conclusions)



---



# 🔍 Overview
This project is a hands-on SQL analysis of a music and mental health survey dataset. The data includes responses from hundreds of people about how they listen to music, what genres they like, how many hours they listen each day, whether they compose or play instruments, alongside self-reported levels of anxiety, depression, insomnia, and OCD.




---

# 🛠️ Tools Used

- **SQL:** For data cleaning, transformation, and analytical querying  
- **SMSS:** Used as the database engine to store and manage the relational dataset   
  

---


# 📦 Dataset


  The dataset used in this project comes from the <strong> Music &amp; Mental Health Survey</strong>, a public dataset available on  <a href="https://www.kaggle.com/datasets/catherinerasgaitis/mxmh-survey-results?resource=download" target="_blank">Kaggle</a>. It includes responses from individuals around the world about their music listening habits, such as favorite genres, streaming platforms, and hours spent listening alongside self-reported measures of mental health like anxiety, depression, insomnia, and OCD.


---

# 🗄️ Database

To manage and explore the dataset effectively, a relational SQL database has been created using Microsoft SQL Server. The schema is designed to reflect the natural structure of the survey, organizing responses into themes like listening habits, genre preferences, and mental health indicators.

Key relationships include:
– Each respondent providing a unique set of answers
– Music preferences connected to self-reported mental health scores
– Streaming behavior linked to demographics like age and daily listening time
– Perceived effects of music categorized alongside listening context and genre



---

# 🧹 Data Processing

The raw CSV file from the Kaggle dataset required some initial cleaning and preparation. 

<br><br>

- Import and load the data into SQL Server Management Studio

  The  dataset file (CSV format) was uploaded directly into SQL Server Management Studio (SSMS) using the "Import Flat File..." wizard. This allowed me to create the table easily with its respective columns and data types, without changing the type.



<img width="830" height="755" alt="image" src="https://github.com/user-attachments/assets/ea3ba7b3-3de0-41d0-aa6d-c5620fa5db1d" />


<br><br>
  
- Handle missing or null values

I’m taking a look at each key table to check for any blank or NULL values. This is a quick way to spot potential data quality issues that might impact the accuracy of the analysis. For every table, I’m counting how many rows are missing important fields with the following code:


<img width="937" height="398" alt="image" src="https://github.com/user-attachments/assets/6dbd8837-73a0-4e45-9134-34a6e6bce9ca" />
<br><br>
Let's have a look at the result:

<img width="1310" height="197" alt="image" src="https://github.com/user-attachments/assets/7c4d1f94-e26a-4f2c-9ee9-2ec5db74fb81" />

Luckily, the dataset is decent, there aren’t many NULL values, so we can move forward without   cleaning.
<br><br>
  
- Simplify formats (e.g., dates)

Here the scope is to change the formats of the field date, we don't really need to know the minute and hour. Let's change it with the CAST function:

<img width="501" height="690" alt="image" src="https://github.com/user-attachments/assets/220e5f6f-9ca1-47a3-b7b6-7c1dafd96152" />


<br><br>
- Drop useless columns (e.g., "Permissions")

This is the code:
<pre>
ALTER TABLE [music-mental-health].dbo.mxmh_survey_results
DROP COLUMN Permissions;
  
</pre>

Let's double check if we truly dropped the column:
<img width="275" height="654" alt="image" src="https://github.com/user-attachments/assets/c52e7acf-f7df-42f2-b2ed-5dfc731fbdd4" />

  

---



# 📈 Project Includes

- **Overview:** This analysis focuses on extracting insights around listening time, platform usage, mood effects, and mental health self-assessments. It’s not just about who listens to what but also it’s about how that might relate to how they feel.
 <br>

Are certain genres more common among people reporting anxiety?:<br>
<img width="502" height="618" alt="image" src="https://github.com/user-attachments/assets/a96d265a-53da-47b0-a61b-a29ff39d0b62" />

<br>

Are certain genres more common among people reporting depression?:<br>
<img width="517" height="599" alt="image" src="https://github.com/user-attachments/assets/e939f73d-3d44-454b-9650-114a818f4769" />
<br>

Do people who listen more hours per day report different mental health patterns?:<br>
<img width="732" height="817" alt="image" src="https://github.com/user-attachments/assets/1084425b-c3c6-4438-8645-4410ac0736ee" />
<br>
Not very clear, let's group using bin:
<img width="972" height="820" alt="image" src="https://github.com/user-attachments/assets/22aa0ca3-ff7d-4768-94c7-f6626cfb7be5" />
Much better. From this result it seems that music is actually worsening our mental health, but it's more plausible that people dealing with more stress or emotional difficulty use music as a coping tool, resulting in longer listening times rather than music causing distress.


<br>
Self report on usefulness of music: <br>
<img width="668" height="439" alt="image" src="https://github.com/user-attachments/assets/c8429bd1-e6c9-4a1f-a17c-b3423c23ab29" />
From a self reporting perspecting it seems that music is very helpful. 
<br>

Are certain genres more commonly associated with mood improvement?
<img width="753" height="750" alt="image" src="https://github.com/user-attachments/assets/461e9cd1-1242-4f4c-9b98-ad9384e1827e" />
From this result we can see that some genres are better performing than others, the best performing are  Gospel and LoFi, while the worst is the videogame music category. (not considering Latin, only 2 respondents)
<br>

<br>
Which streaming service had the most improving users and which one the most worsening?:
<img width="731" height="539" alt="image" src="https://github.com/user-attachments/assets/5bb4f7eb-e175-4c86-8433-83ffbec095b5" />
The best streaming service with the highest improving users percentage seems to be Pandora, followed by Spotify.
<br><br>


# Conclusion
<br>
While it’s widely accepted that music can have a positive impact on mental health, it’s much harder to pin down exactly how that works or what kind of music helps most. People's preferences, listening habits, and emotional responses vary so much that drawing clear lines between genres and mental health outcomes is complicated. This project doesn’t try to prove anything definitive, but instead looks at what the data might suggest where patterns start to emerge, and where things remain personal and subjective.


<br><br>
---
<br><br>
