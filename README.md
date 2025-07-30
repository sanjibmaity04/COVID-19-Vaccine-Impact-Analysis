COVID-19 Vaccine Impact Analysis
This repository contains a data analysis project focused on exploring the global rollout of COVID-19 vaccines and their observed relationship with public health outcomes. It leverages publicly available data to identify trends, correlations, and potential insights into the pandemic's trajectory.

<img width="1920" height="1280" alt="image" src="https://github.com/user-attachments/assets/d74bba28-d7b7-46cc-9a71-98428c13842b" />
Table of Contents
Project Overview

Features--->

Ethical Considerations & Data Sourcing--->

Technologies Used---->

Project Structure--->

Installation---->

Usage---->

Key Analysis Areas--->

SQL Integration---->

Pandas & NumPy Implementation--->

Example Insights--->

Contributing--->

<img width="870" height="490" alt="image" src="https://github.com/user-attachments/assets/f8248b53-624f-4450-943c-a2e50740f60c" />

>>>>>Project Overview:<<<<

The COVID-19 pandemic presented unprecedented global health challenges. This project aims to analyze the extensive data collected during the pandemic, specifically focusing on the relationship between vaccination rates and public health outcomes such (as new cases and deaths) across different countries and over time. We also explore how socioeconomic factors might have influenced vaccination uptake.

The primary goal is to provide data-driven insights into the observed impact of vaccination efforts, using a robust data analysis pipeline that includes data acquisition, cleaning, transformation, and visualization.

Features:

Data Acquisition: Automated download of a comprehensive global COVID-19 dataset.

SQL Database Integration: Loading raw data into a local SQLite database for structured storage and efficient querying.

Data Cleaning & Preprocessing: Handling missing values, correcting data types, and preparing data for analysis using Pandas and NumPy.

Feature Engineering: Creating new, insightful metrics (e.g., per capita cases/deaths, vaccination rates) to facilitate deeper analysis.

Exploratory Data Analysis (EDA): Identifying trends, patterns, and correlations through statistical summaries and visualizations.

Visualization: Creating informative plots to communicate key findings effectively.

Reproducible Workflow: A Jupyter Notebook guides the entire analysis process, ensuring transparency and ease of replication.

Ethical Considerations & Data Sourcing
This project adheres to strict ethical guidelines:

Data Privacy:  We use only aggregate, publicly available data. No individual-level patient data is accessed or analyzed.

Data Source: The primary dataset is the owid-covid-data.csv from Our World in Data (OWID), a highly reputable source that aggregates data from official national and international bodies (e.g., WHO, CDC, national health ministries).
<img width="631" height="791" alt="image" src="https://github.com/user-attachments/assets/147a4f1a-4486-4919-a0f7-c499e278c3ea" />


Interpretation: The analysis focuses on observed correlations and trends, not definitive causation. Establishing causal links requires rigorous epidemiological studies beyond the scope of this project.

Data Recency: Given that official daily reporting on COVID-19 has scaled back in many regions by mid-2025, the analysis focuses on historical data up to early 2024 (or the latest widely available complete datasets) to provide stable trends and insights.

Technologies Used
Python 3.x

Pandas: For powerful data manipulation, cleaning, and analysis.

NumPy: For high-performance numerical operations and vectorized computations, forming the backbone of Pandas' efficiency.

SQLite3: A lightweight, file-based SQL database for local data storage and querying.

Matplotlib: For creating static, high-quality visualizations.

Seaborn: Built on Matplotlib, for attractive and informative statistical graphics.

Jupyter Notebook: For interactive development, analysis, and presentation.

Requests: For downloading the dataset from the web.

Project Structure
COVID19-Vaccine-Impact-Analysis/
├── README.md
├── requirements.txt
├── data/
│   ├── owid-covid-data.csv         # Downloaded raw data
│   └── covid_impact_database.db    # Generated SQLite database
├── notebooks/
│   └── vaccine_impact_analysis.ipynb # Main Jupyter Notebook for analysis
├── src/
│   ├── database_utils.py           # Python functions for DB interaction
│   └── data_cleaning_prep.py       # Python functions for data cleaning and feature engineering
└── .gitignore                      # Specifies files/folders to ignore in Git

Installation
To set up and run this project locally, follow these steps:

Clone the repository:

git clone https://github.com/your-username/COVID19-Vaccine-Impact-Analysis.git
cd COVID19-Vaccine-Impact-Analysis

(Remember to replace your-username with your actual GitHub username.)

Create a virtual environment (recommended):

python -m venv venv
source venv/bin/activate  # On Windows: `venv\Scripts\activate`

Install the required Python packages:

pip install -r requirements.txt

Usage
The core analysis is performed within the notebooks/vaccine_impact_analysis.ipynb Jupyter Notebook.

Start Jupyter Notebook:

jupyter notebook

In your browser, navigate to and open notebooks/vaccine_impact_analysis.ipynb.

Run all cells sequentially. The notebook is designed to:

Automatically download the latest OWID COVID-19 data.

Set up and populate the SQLite database (data/covid_impact_database.db).

Load data from the database into Pandas DataFrames.

Perform all data cleaning, preprocessing, and analysis steps.

Generate visualizations.

Key Analysis Areas
The project explores the following aspects:

Global Vaccination Rollout: Tracking the cumulative number of vaccinations and fully vaccinated individuals over time.

Country-Specific Trends: Detailed analysis of selected countries, comparing their vaccination progress with new case and death rates.

Correlation Analysis: Investigating the statistical relationship between vaccination rates and public health outcomes (e.g., lower cases/deaths).

Socioeconomic Factors: Exploring how indicators like GDP per capita, population density, or healthcare access might correlate with vaccination coverage.

SQL Integration
This project utilizes SQLite as a simple, file-based database. The src/database_utils.py script and the Jupyter Notebook demonstrate basic SQL operations:

Connecting to the Database: Establishing a connection to covid_impact_database.db.

Creating Tables: Dynamically creating the covid_data table schema based on the Pandas DataFrame.

Inserting Data: Efficiently populating the covid_data table from the downloaded CSV using Pandas' to_sql() method.

Basic SELECT Queries: Retrieving specific subsets of data (e.g., SELECT * FROM covid_data WHERE location = 'India') into Pandas DataFrames using pd.read_sql_query(). This showcases how SQL is used for efficient data extraction before Python takes over for deeper analysis.

Pandas & NumPy Implementation
This project heavily relies on Pandas for structured data manipulation and NumPy for high-performance numerical computing:

DataFrames (pd.DataFrame): The core data structure used throughout the project for tabular data.

Data Loading: pd.read_csv() for initial file reading, and pd.read_sql_query() for loading data from SQL into DataFrames.

Data Cleaning:

pd.to_datetime(): Converting date strings to datetime objects for time-series analysis.

.dropna(), .fillna(): Handling missing values with various strategies.

.drop_duplicates(): Ensuring data integrity by removing redundant entries.

pd.to_numeric(): Ensuring numerical columns are correctly typed.

Data Transformation & Feature Engineering:

Pandas vectorized operations (NumPy-powered): Efficiently calculating new columns like new_cases_per_million or people_fully_vaccinated_per_hundred using direct arithmetic operations on entire Series (e.g., (df['column'] / df['population']) * 1_000_000). These operations are highly optimized by NumPy.

np.where(): A NumPy function used for conditional logic in column creation, preventing division by zero or handling specific edge cases in numerical calculations.

.groupby(): Grouping data by location, date, or continent to perform aggregate calculations (.sum(), .mean(), .median()).

.rolling().mean(): Calculating rolling averages (e.g., 7-day average of new cases) for trend smoothing.

.resample(): Resampling time-series data (e.g., monthly totals) for trend analysis.

Analysis:

.describe(): Generating summary statistics for numerical columns, which uses NumPy internally.

.corr(): Calculating correlation matrices between different metrics (e.g., vaccination rate and death rate). This Pandas method relies on NumPy's efficient correlation algorithms.

.nlargest(): Identifying top-performing or most impacted entities.

Example Insights (Potential Findings)
Based on the analysis, you might find insights such as:

Clear inverse relationship: A general trend where increasing vaccination rates are associated with a decrease in new cases and deaths per million population in many countries.

Disparities in Rollout: Differences in vaccination coverage and speed across continents or between countries with varying GDP per capita or healthcare infrastructure.

Impact of Socioeconomic Factors: A positive correlation between higher GDP per capita or hospital bed availability and higher vaccination rates.

Waning Immunity/Variants: Evidence of new waves of cases even in highly vaccinated populations, suggesting the influence of new variants or waning vaccine effectiveness over time.

Data Limitations: Acknowledgment of challenges like inconsistent reporting, data gaps, or the difficulty of isolating vaccine impact from other public health interventions.

Contributing
Contributions, suggestions, and feedback are welcome! If you have ideas for improvements, new features, or bug fixes, please open an issue or submit a pull request.

License
This project is open-sourced under the MIT License. See the LICENSE file (if you create one) for more details.
