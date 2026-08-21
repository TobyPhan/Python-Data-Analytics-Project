# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles, I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here:
[2_Skills_Demand.ipynb](Project\2_Skills_Count.ipynb)


### Visualize Data
```python

fig, ax = plt.subplots(len(job_titles), 1)
for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 78)
    # remove the x-axis tick labels for better readability
    if i != len(job_titles) - 1:
        ax[i].set_xticks([])
    # label the percentage on the bars
    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n, f'{v:.0f}%', va='center')

fig.suptitle('Likelihood of Skills Requested in US Job Postings', fontsize=15)
fig.tight_layout(h_pad=.8)
plt.show()
```

### Results
![Visualization of Top Skills for Data Roles](Project/Images/Skill_Demand_all_Data_roles.png)


### Insights

- Python is a very versatile skill, highly demanded across all 3 roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).
- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over 50% of the job postings for both roles. For Data Engineers though, Python is the most sought-after skill, appearing in 68% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data mangement and analysis tools (Excel, Tableau).

## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data

```python
from matplotlib.ticker import PercentFormatter
df_plot = df_DA_US_percent.iloc[:, :5]

sns.lineplot(data = df_plot, dashes = False, palette = 'tab10', legend= 'full')
sns.set_theme(style = 'ticks')
sns.despine()

plt.title('Trending Top Skills for Data Analysts in the US')
plt.ylabel('Likelihood of Job Postings')
plt.xlabel('2026')
plt.legend().remove()

ax= plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals = 0))

for i in range(5):
    plt.text(11.2,df_plot.iloc[-1,i],df_plot.columns[i])
plt.show()
```
### Results

![Trending Top Skills for Data Analysts in the US in 2025](Project/Images/Skill_Trend_DA.png)

*Bar graph visualizing the trending top skills for data analysts in the US in 2025.*

### Insights
- SQL remains the most consistenly demanded skill throughout the year, although it shows a gradual decrease in demand throughout the year.
- Excel experienced a similar trend with SQL, showing a decline in demand and sharper decline starting in August.
- Tableau and Python show relatively stable demand and show the same trend against each other with some fluctuations. In August, Python slightly edges out Tableau during that month, but Tableau bounces back.
- SAS shows a stable trend throughout the year at relatively 20%.

All these technologies are safe for the time being to learn.


