# The Analysis
## 1. What are the most demanded skills for the top 3 most popular data roles?
To find the most demanded skills for the top 3 most popular data roles, I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here: [2_Skills_Count.ipynb](2_Skills_Count.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_sckills_pct[df_sckills_pct['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:g_r')

plt.show()
```

### Results
![Visualization of Top Skills for Data Nerds](images/skill_count_result.png)

### Insights
- Python is a versatile skill, highly demanded accross all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).
- SQL is the most requested skill for Data Analysis and Data Scientists, with it in over half the job postings for both roles. For Data Engineers, Python is the most sought-after skill, appearing in 68% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).


## 2. How are in-demand skills trending for Data Scientists?

### Visualize Data

```python

from matplotlib.ticker import PercentFormatter

df_plot = df_DS_US_pct.iloc[:, :5]
sns.lineplot(df_plot, dashes=False, palette='tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decilas=0))

plt.show()

```

### Results
![Trending Top Skills for Data Scientists in the US](images/skill_trend_result.png)
*Line graph visualizing the trending top skills for data scientists in the US in 2023*

### Insight:
- Python is the dominant skill for data scientists, remaining significantly higher than all other skills.
- SQL and R are both important but show a slight decline in demand, indicating a possible shift in the industry toward Python as a more versatile tool.
- SAS and Tableau are useful but niche tools, ranking much lower in job postings, suggesting these may be more specialized or supplementary skills rather than core competencies for data science.

In summary, the chart highlights that mastering Python and SQL is crucial for data scientists, while familiarity with R, SAS, and Tableau can provide added value depending on the specific role or industry.