# Data Job Market Analysis

> **Summary:** A SQL + Python analysis of data-job postings that compares skill demand (number of postings) against pay (average yearly salary) to show which skills are worth learning.
>
> **Tech stack:** PostgreSQL, SQL, Python, pandas, Matplotlib, Jupyter

![Job market overview: average salary and number of postings by job title](assets/job_market_overview.png)

## Project Overview
This project analyzes the data job market by looking at the relationship between market demand (number of job postings) and compensation (average yearly salary), to find the "sweet spot" for career growth and skill acquisition.

The goal of this analysis was to move beyond anecdotal evidence and use data to determine which skills offer the highest return on investment for data professionals.

Link for data: https://drive.google.com/drive/folders/1moeWYoUtUklJO6NJdWo9OV8zWjRn0rjN

## Key Findings
Numbers below are from the saved outputs of `notebooks/1_visualize_data.ipynb`.

* **SQL is the most in-demand skill for Data Analysts.** It appears in 92,628 Data Analyst postings, ahead of Excel (67,031), Python (57,326), Tableau (46,554) and Power BI (39,468).
* **Seniority pays.** Among postings that list a salary, the highest average yearly salaries by job title are Senior Data Scientist ($154,050, 1,686 postings) and Senior Data Engineer ($145,867, 1,594 postings), compared with $135,929 for Data Scientist (5,926 postings) and $130,267 for Data Engineer (4,509 postings).

## Approach
* **Quadrant analysis:** plots skills (or job titles) by postings and average salary against the medians to separate high-demand, high-pay skills from the rest.
* **Role-specific trends:** compares Data Analyst postings with the broader "Data" field to show how skill requirements shift across roles.
* **Baseline vs. specialized skills:** high-volume, lower-salary skills such as Excel and SQL show up as baseline requirements, while specialized tools such as TensorFlow, Kubernetes and PyTorch appear among the highest-paying remote skills (about $153K average each, in skills with more than 100 postings).

## Visualizations

![Quadrant Analysis of Job Market](assets/quadrant_analysis_of_job_market_overview.png)
![Top Skills for All Data Jobs](assets/top_skills_in_data.png)
![Top Skills for Data Analyst Jobs](assets/top_skills_data_analyst.png)
![Skills with Highest Demand](assets/highest_demand_skills.png)
![Most Optimal Skills using Quadrant Analysis](assets/quadrant_analysis_skills.png)

## Repository Structure

```text
data-job-market-analysis/
├── assets/          # Exported visualizations
├── csv_files/       # Datasets and exported query results (git-ignored, not in the repo)
├── notebooks/       # Jupyter notebook with the charts
├── sql_load/        # Scripts that create the database and tables and load the data
├── sql_queries/     # SQL queries used to aggregate the data
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

## How to Run This Project

The data is not stored in the repo, so the pipeline is: load the data into PostgreSQL, run the queries, export the results to `csv_files/`, then open the notebook.

1. **Clone the repository:**
   ```bash
   git clone https://github.com/vdd11/data-job-market-analysis.git
   cd data-job-market-analysis
   ```
2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
3. **Get the data:** download the dataset from the link above into a local `csv_files/` folder.
4. **Load it into PostgreSQL:** run the scripts in `sql_load/` in order (`1_create_database.sql`, `2_create_tables.sql`, `3_modify_tables.sql`). **Edit the file paths in the `COPY` statements in `3_modify_tables.sql`**, which point to a local folder on the author's machine.
5. **Run the queries** in `sql_queries/` and export each result as a CSV into `csv_files/`. The notebook reads these files: `highest_paying_job_titles.csv`, `highest_paying_skills_all.csv`, `highest_paying_skills_data_analyst.csv`, `highest_skill_demand_all.csv`, `highest_skill_demand_data_analyst.csv`, `optimal_skills_all_remote.csv` and `optimal_skills_data_analyst_remote.csv`. The `*_data_analyst*` files appear to be Data Analyst-only versions of these queries, but the repo only contains the all-jobs versions. [TODO: add the Data Analyst query variants.]
6. **Launch the notebook:**
   ```bash
   jupyter notebook notebooks/
   ```

## License

MIT. See [LICENSE](LICENSE).
