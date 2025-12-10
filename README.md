# Digital Strategy Analysis: The Grammys & Recording Academy

## 📌 Project Overview
**Objective:** To evaluate the effectiveness of The Recording Academy's digital restructuring (splitting `grammy.com` and `recordingacademy.com`).

**Context:** I analyzed web analytics data to determine if separating the "fan-facing" site from the "professional" site improved user engagement metrics like Bounce Rate and Session Duration.

***Note:*** *The raw dataset for this project is not included in this repository due to privacy constraints. This repository serves as a showcase of the Python logic, data manipulation techniques, and visualization code structure used in the analysis.*

## 🛠️ Tools & Libraries
* **Python (Pandas):** Used for data cleaning, merging multiple datasets (`pd.concat`), and time-series manipulation.
* **Plotly Express:** Used for creating interactive visualizations to track user journey trends.
* **Jupyter Notebook:** The environment used for Exploratory Data Analysis (EDA).

---

## 💻 Technical Implementation
*Below are the key logic blocks used to derive insights from the raw web analytics data.*


###  Data Aggregation & Cleaning
The challenge was to merge separate analytics exports while preserving the distinction between the two domains. I utilized `pd.concat` for an efficient union and standardized the timestamp formats for accurate time-series plotting.

```python
# Merging the two datasets (Grammys vs. Recording Academy)
# 'keys' argument adds a top-level index to distinguish the data sources
concat_df = pd.concat([grammys_df, ra_df], keys=['Grammys', 'Recording Academy'])

# Converting 'date' to datetime objects for time-series plotting
concat_df['date'] = pd.to_datetime(concat_df['date'])

# Inspecting the merged structure
print(f"Total Records Analyzed: {concat_df.shape[0]}")
2. Metric Engineering
```
To measure "Stickiness," I created a custom calculated field. This metric helps quantify how valuable a user found the content relative to the time they spent on the page.


```python
# Creating a calculated field for engagement (Duration per Pageview)
# This normalizes the data to identify high-quality traffic sources
concat_df['engagement_score'] = concat_df['avg_session_duration'] / concat_df['pageviews']
3. Visualization Logic (Plotly)
```
I utilized Plotly Express for its interactivity. The code below was designed to generate a line chart tracking the specific impact of the "Awards Night" marketing push.

```python
# Visualizing the traffic surge across both domains
fig = px.line(
    concat_df, 
    x='date', 
    y='visitors', 
    color='domain_name',  # Split lines by website
    title='Daily Visitors: Pre vs Post Grammys'
)

# Customizing layout for stakeholder presentation
fig.update_layout(
    xaxis_title='Date', 
    yaxis_title='Total Visitors',
    template='plotly_white'
)
fig.show()
```


### Summary of Findings
Although the raw visualizations cannot be rendered here without the dataset, the analysis yielded the following data-driven insights:

- **Traffic Surge**: Identified a massive 42x increase in traffic on awards night (peaking at ~1.3M visitors).

- **Strategy Validation**: The strategic split reduced the professional site's bounce rate to 33.6% (down from a combined average of 41.6%), proving that industry professionals prefer a dedicated workspace.

- **Engagement Win**: Average session duration increased by 40 seconds on the professional domain, indicating higher content relevance.

### Recommendations
Based on the code output, I recommended:

- Retain the Domain Split: The lower bounce rate validates the dual-site strategy.

- Post-Event Retention: Implement a "Day-After" content strategy on the professional site to capture and retain the viral traffic spillover from the awards show.