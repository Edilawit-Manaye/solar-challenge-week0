# Interim Report: Week 0 Plan - Solar Challenge

## Project Title: Solar Farm Data Analysis

**Date:** [Insert Current Date, e.g., October 26, 2023]
**Author:** [Your Name]
**GitHub Repository:** [Your GitHub Repository Link, e.g., `https://github.com/Edilawit-Manaye/solar-challenge-week0`]

---

## 1. Introduction

This interim report outlines the plan and progress made during Week 0 of the Solar Farm Data Analysis project. The primary objectives for this phase were to establish a robust development environment, implement version control best practices, and begin the Exploratory Data Analysis (EDA) for the provided solar farm datasets from Benin, Sierra Leone, and Togo.

---

## 2. Task 1 Summary: Git & Environment Setup

The initial phase focused on establishing a robust version control system and a reproducible Python development environment. This involved the following key steps, with details also documented in the `README.md` file:

### 2.1. Repository Initialization and Cloning
A new GitHub repository named `solar-challenge-week0` was created to host the project. The repository was subsequently cloned locally to the development machine using the command:
```bash
git clone https://github.com/yourusername/solar-challenge-week0.git
cd solar-challenge-week0




2.2. Virtual Environment Setup
A Python virtual environment was created to manage project-specific dependencies in isolation, preventing conflicts with other Python projects. This was achieved with:
code
Bash
python -m venv venv
The virtual environment was then activated. On Windows, this was done via venv\Scripts\activate, and on macOS/Linux, it was source venv/bin/activate.
2.3. Dependency Management
A requirements.txt file was set up at the project root to explicitly list all necessary Python packages. This ensures that the environment can be easily reproduced. The required dependencies, including pandas, numpy, matplotlib, seaborn, scipy, notebook, etc., were installed using:
code
Bash
pip install -r requirements.txt
2.4. Version Control Best Practices
A .gitignore file was configured to exclude irrelevant or generated files from version control. This includes the venv/ directory, the data/ directory (where raw and cleaned CSVs reside), and Jupyter notebook checkpoints (.ipynb_checkpoints/). Development work was conducted on feature branches (e.g., setup-task), and commits were made with descriptive messages following conventional commit guidelines (e.g., "feat: implement initial EDA for Benin", "chore: update requirements.txt").
2.5. Continuous Integration (CI) Setup
A basic GitHub Actions workflow (.github/workflows/ci.yml) was implemented. This workflow automates a preliminary check upon pushes and pull requests, specifically ensuring that project dependencies can be installed correctly via pip install -r requirements.txt. This step confirms the reproducibility of the environment.
2.6. Documentation
The README.md file was updated with comprehensive instructions for setting up the environment, running the notebooks, and understanding the project structure.
2.7. Branch Merging
The feature branch dedicated to setup tasks (setup-task) was successfully merged into the main branch via a Pull Request, marking the completion and integration of the environment setup.
3. Task 2 Approach: Data Profiling, Cleaning & EDA Outline
Task 2 involves a comprehensive Exploratory Data Analysis (EDA) for the solar farm datasets from Benin, Sierra Leone, and Togo. This process is systematically carried out within three distinct Jupyter notebooks located in the notebooks/ directory: benin_eda.ipynb, sierraleone_eda.ipynb, and togo_eda.ipynb. The general approach for each country's dataset is as follows:
3.1. Data Loading and Initial Inspection
Each notebook begins by loading its respective raw CSV file (e.g., benin-malaniville.csv) into a pandas DataFrame. The 'Timestamp (yyyy-mm-dd hh:mm)' column is consistently renamed to 'Timestamp' and converted to datetime objects to facilitate time-series analysis. A quick df.head() provides an initial glimpse into the dataset's structure and content.
3.2. Summary Statistics & Missing-Value Report
Fundamental descriptive statistics (df.describe()) are generated for all numerical columns to understand data distribution, central tendencies (mean, median), and variability (standard deviation). A detailed missing-value report is compiled, calculating both the count and percentage of NaN values for each column. Columns with more than 5% missing data are specifically highlighted as areas requiring careful attention during cleaning.
3.3. Outlier Detection & Basic Cleaning
Numeric columns identified as critical for solar performance and environmental conditions (e.g., GHI, DNI, DHI, ModA, ModB, WS, WSgust) are targeted for outlier detection. Before Z-score calculation, any existing missing values within these columns are imputed using their respective medians to ensure robustness. Z-scores are computed, and data points with an absolute Z-score greater than 3 are flagged as potential outliers. For non-numeric columns like 'Comments', missing values are filled with a descriptive placeholder ('No Comments'). The cleaned DataFrame for each country is then saved as a new CSV file (e.g., benin_clean.csv) in the data/ directory.
3.4. Time Series Analysis
This section focuses on understanding temporal patterns. Line plots are generated to visualize trends of solar irradiance (GHI, DNI, DHI) and ambient temperature (Tamb (°C)) over time. Further analysis involves grouping data by month and hour of the day to identify seasonal variations and diurnal cycles in average GHI, providing insights into peak performance periods.
3.5. Cleaning Impact Analysis
The impact of cleaning events on solar module performance is assessed. Bar plots illustrate the average ModA (W/m²) and ModB (W/m²) values, comparing periods with and without cleaning (based on the 'Cleaning (1 or 0)' column). Standard deviation error bars are included to indicate the variability around these averages.
3.6. Correlation & Relationship Analysis
A correlation heatmap is generated for a selection of key numerical variables, providing a visual overview of their linear relationships. Additionally, scatter plots are used to specifically visualize relationships between pairs of variables, such as Wind Speed vs. GHI, Wind Gust vs. GHI, and Relative Humidity vs. Ambient Temperature, to discern direct or inverse correlations and potential influences.
3.7. Wind & Distribution Analysis
Histograms are created for crucial variables like GHI and Wind Speed to examine their frequency distributions. For wind analysis, a radial bar plot (or a simplified wind rose) displays the average wind speed categorized by wind direction, helping to identify prevailing wind patterns and their strengths.
3.8. Temperature Analysis (Influence of RH on Temp and GHI)
The interplay between relative humidity (RH (%)), ambient temperature (Tamb (°C)), and global horizontal irradiance (GHI (W/m²)) is explored. A scatter plot is utilized where the color and size of data points are mapped to GHI, illustrating how humidity and temperature interact and potentially affect solar radiation capture.
3.9. Bubble Chart: GHI vs. Tamb with Bubble Size = RH
A multi-dimensional bubble chart is created, plotting GHI against Ambient Temperature. In this visualization, the size and color of each bubble represent the Relative Humidity. This advanced plot provides a comprehensive view of how these three critical environmental factors interact and influence solar performance.
