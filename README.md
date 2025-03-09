# The Analysis

## What are teh most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles, I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I’m targeting.

View to my notebook with detailed steps here: [2.skill_counting.ipynb](project/2.skill_counting.ipynb)

### Visualize Data

```python
for i, job_title in enumerate(job_titles):
  df_plot = df_skills_perc[df_skills_perc['job_title_short']==job_title].head(5)
  sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
  ax[i].set_ylabel('')
  ax[i].set_xlabel('')
  ax[i].get_legend().remove()
  ax[i].set_xlim(0, 78)

  for n, v in enumerate(df_plot['skill_percent']):
    ax[i].text(v+1, n, f'{v:.0f}%', va='center')

  if i != len(job_titles)-1:
    ax[i].set_xticks([])
```

### Result

![Visualization of Top Skills](project/images/skill_demand_all_data_roles.png)

### Insights

- Python is critical for Data Scientists and Data Engineers but less so for Data Analysts – Python appears in 72% of Data Scientist job postings and 65% of Data Engineer postings, making it the dominant programming language for these roles. However, for Data Analysts, it is only mentioned 27% of the time, suggesting it is less of a core requirement.
- SQL is the most universally required skill across all three roles – It appears in over half of job postings (51%) for Data Analysts and Data Scientists, and is also highly demanded (65%) for Data Engineers.
- Data Analysts rely more on Excel and Tableau for data visualization and reporting – Excel (41%) and Tableau (28%) are commonly listed for Data Analysts, reinforcing the need for strong data visualization and reporting skills in this role.
- Cloud and big data technologies are more important for Data Engineers – Skills like AWS (43%), Azure (32%), and Spark (32%) appear primarily in Data Engineer postings, highlighting the importance of cloud platforms and distributed computing in engineering roles.

# The Analysis

## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data

```python
from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

from adjustText import adjust_text

texts = []
for i in range(5):
    y_pos = df_plot.iloc[-1, i]

    # Move "Python" label down slightly
    if df_plot.columns[i] == "python":
        y_pos -= 2  # Adjust downward by 2 units (you can change this)

    texts.append(plt.text(11.2, y_pos, df_plot.columns[i]))
```

### Results

![Trending Top Skills for Data Analysts in the US](project/images/trending_skills.png)
_Bar graph visualizing the trednding top skills for data analysts in the US 2023_

### Insights:

- SQL remains the most in-demand skill for data analysts in the US, consistently leading at above 50% throughout the year, though it shows a slight decline towards the end of the year.
- Excel holds a strong second position with a steady demand of around 40-45%, but it drops significantly toward the last quarter before rebounding in December.
- Tableau and Python are competing closely in the mid-tier range (~25-30%). Tableau sees a peak in August, whereas Python trends downward in the last quarter, possibly indicating a shift in preferred visualization or programming tools.
- SAS has the lowest demand among the top 5 skills, remaining stable around the 20% mark with minor fluctuations.
