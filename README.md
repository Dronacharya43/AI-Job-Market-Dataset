# AI Job Market Dashboard — Power BI Project

A Power BI dashboard that analyzes AI/ML job market trends from 2020 to 2026. I built it while learning Power BI by working with a real dataset instead of following a tutorial.

<img src="AI Job Market Dashboard.png" alt="Dashboard">

## 🔍 Key Insight

Even though Python is widely believed to be the most in-demand skill in AI/ML hiring, it ranked **last** among the five main skills tracked in this dataset. Cloud and Machine Learning skills were the most in demand instead.

## 📊 What's in the Dashboard

* **KPI overview** — total job postings, YoY growth %, and average salary by role
* **Monthly posting trends** — hiring volume over time, showing clear seasonal patterns
* **Skill demand** — number of job postings by required skill (Cloud, ML, SQL, Deep Learning, Python)
* **Role breakdown** — job postings and average salary by job title
* **Industry mix** — number of job postings by industry and company size

## 🛠️ Built With

* Power BI Desktop
* Power Query (data cleaning, unpivoting, data modeling)
* DAX (measures and time intelligence)

## 📁 Dataset

[AI & Data Science Job Market Dataset (2020–2026)](https://www.kaggle.com/datasets/shree0910/ai-and-data-science-job-market-dataset-20202026) — public dataset from Kaggle.

## 🧠 What I Learned

This was my first project-based build in Power BI that was not based on a tutorial. These are some things I had to solve myself instead of just following along:

**Data modeling**

* Combined separate month and year whole-number columns into a real `Date` using `#date()` in Power Query because direct type conversion reads whole numbers as date serial numbers.
* Changed wide skill columns (`skills_python`, `skills_sql`, etc.) into a long `Skill` column using unpivoting. I also faced a real problem: unpivoting directly in the main table caused job postings to be counted double or triple (10K → 28K) because one posting could now have multiple rows. I fixed this by splitting the data into two linked tables: `Postings` for counts, salary, and time, and `Skills` for skill-level analysis. The tables were joined using the posting ID.

**DAX**

* Learned to use `COUNTROWS()` for row-based counts and how a measure automatically recalculates based on filter context (slicers and chart axes) instead of being fixed for each category.
* Used `CALCULATE()` + `SAMEPERIODLASTYEAR()` to calculate real year-over-year growth — the main pattern behind most time intelligence in DAX.
* Used `RANKX()` for dynamic ranking and learned why it needs a real column with category values, not column headers, to rank categories.

**Chart design**

* Found and fixed a truncated Y/X-axis that did not start at 0. This was visually making the differences between categories look bigger — a common way bar and line charts can unintentionally mislead.
* At first, I used a waterfall chart to compare independent skill categories. I learned that waterfall charts are meant to show cumulative changes in one value across sequential steps, not to compare unrelated categories side by side. I changed it to a clustered column chart instead.

## 📂 Files

* `AI Job Market.pbix` — the Power BI file
* `AI Job Market Dashboard.png` — a static preview image

## 📬 Feedback Welcome

I am still early in my Power BI journey. If you notice anything I could improve (DAX, modeling, or design), I would genuinely appreciate your feedback.
