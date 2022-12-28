# Expect life - A project about Life Expectancies and Social Security Systems

## Project Overview
This is a team project for data exploration, data analysis, and presentation of findings through a dashboard and visuals.

### Proposal
**Topic**: Life expectancy for nations around the world, and connections to the national social security system.

Questions to be answered by this project: 

* Does the type of social security system impact life expectancy?
* Does the amount of healthcare funding impact life expectancy?
* Does a country's GDP impact life expectancy?
* How big of a role do selected lifestyle factors (for example, alcohol consumption, smoking) play in life expectancy?
* What portion of differences in life expectancy is caused by young deaths (under 65)?
* Other questions - TBD

**Selection Rational**: There are continuing discussions in American politics about the need for changes in the national healthcare system.  Elections have seen candidates propose the adoption of Universal Healthcare or other similar large-scale changes.  This project seeks to explore whether the type of national healthcare system can affect the longevity of the population.  This will be explored with data from nations around the world.

After reviewing the available data, we saw that there was only healthcare system data available for less than half of the world's nations.  However, there is information available about almost all the world's social security systems.  The social security systems include healthcare as well as providing money for retirement and assistance for accidents and emergencies.

This study focuses on the social security programs associated with health (Sickness and Maternity), but can include information about retirement systems, such as for North Macedonia, where the country does not indicate a separate social security system for health.

#### [Google Slides Presentation](https://docs.google.com/presentation/d/1GDFdQnD2gt4tPtTPS35o6d5ekbh1FRK6IDjy1pRzjho/edit?usp=sharing)

#### [Tableau Dashboard](https://public.tableau.com/app/profile/vivek.gurumoorthy7572/viz/Life_Expectancy_16711432013830/LifeExpectancyDash?publish=yes)

#### Social Security System Definitions
* Individual account: (may be mandatory or optional)
* Notional defined contribution (NDC)
* Occupational pension system:
* Provident fund:
* Social assistance system:
* Social insurance system:
* Universal system: (system components are identified separately)



## Input Data
Input data was sourced from multiple locations:
* Life Expectancy data was collected from the World Bank.
* GDP data was also collected from the World Bank.
* Social Security system data was collected from ISSA (The International Social Security Association)

### Input Data Issues
We frequently encountered data that was missing data values.  Sometimes for specific metrics in specific years, and other times for collections of metrics within one or more countries.

![Data pre-processing - missing values](./Resources/data-preprocessing-missing-values.png)


Another issue that we frequently encountered was data that included general geographic regions, in addition to listing the individual countries.  Because the primary Life Expectancy data and social security system data was oriented towards individual countries, the regional data was processed out of the input data before bringing this information into the database and machine-learning model.

Additionally, there were frequent issues with the individual country names.  This was due to a number of factors, such as, accented characters within the country name, for example `Côte d'Ivoire`, and the fullness of country names, such as, `Democratic Republic of the Congo` vs. `Congo, Democratic Republic`.

![Data pre-processing - reconciling country names](./Resources/data-preprocessing-reconciling-countries.png)

#### Gross Domestic Product
The resulting data file contained all of the countries that aligned with the Social Security System data.  Within this collection of countries, the following were dropped because of missing information: British Virgin Islands, Jersey, Slovakia, Taiwan (China), and Venezuela.

### Team Structure and assignments:  
The team has made the following decisions:
* AZ to serve as the project manager
* Team members will work in pairs.  Weeks 1&2: (Jay & Vivek), (AZ & David) - these teams may change in the latter half of the project.
* Google sheet started to collect team availability.  We expect to meet at least every other day for a short stand-up, and have the option to extend or reconvene for more discussion/working sessions.
* All team communication and collaboration held over email, Slack, and Google Meet or Hangouts. 

### Technology: 
* Data Exploration: Python/Pandas/Jupyter Notebook.
* Database: MongoDB free tier - M0 cloud database
* Machine Learning: Python & Scikit-Learn.  Maybe also Tensorflow.
* Presentation: Tableau

## Architecture and Design
The high-level archictecture for this project is depicted below:

![High-Level Architecture](./Resources/hl-architecture.png)

#### Architecture and Design Description
The Dashboard will be presented to the user via Tableau Public.  Tableau may connect to the MongoDB, or be provided data in CSV format.  The Machine Learning model will interact with the PostgreSQL database to collect the input data and provide results back to the database.

Below is a high-level diagram of the User Interface/Dashboard:
![High-Level UI/Dashboard](./Resources/HL-presentation-diagram.png)


## Deliverables:


### Database: 
* MongoDB Cloud Database - We decided this is the best option for the collection of data we are gathering and processing for this project. 
    * The collected project input data will not exceed the limitations of the minimal environment.  

    ![Database](./Resources/database_data1.png)

We are working with a subset of our data that was imported into the database.

![Database Data](./Resources/database_data-detail.png)


Below is a list of features we identified and will use for our analysis.
- Age 
- Gender
- Population
- GDP (USD)
- Tobacco use
- Alcohol use
- Daily Protein Supply


### Machine Learning Model
* Machine Learning Model - will evaluate the data features and provide information about the feature importance, as well as clustering of features that contribute to Human Longevity.
* Currently, the machine learning model is using PCA for feature reduction, and KMeans for clustering analysis

Because the data under investigation is based on individual countries, the data set is wide (523 feature columns).  To help generate graphable results, Principal Component Analysis (PCA) was used to reduce the feature set down to three primary components.

![Principal Component Analysis](./Resources/machine_learning-clustering-attempt_1-PCA.png)

An Elbow Curve diagram was then generated to help determine the likely number of clusters.

![Elbow Curve](./Resources/machine_learning-clustering-attempt_1-Elbow_Curve.png)

Based on this diagram, n_clusters was set to 3, and then the clusters were predicted.

![KMeans Clusters](./Resources/machine_learning-clustering-attempt_1.png)

Because the data was abstracted through the use of PCA, it is difficult to interpret the clustering results.

![Clustering Interpretation](./Resources/cluster-interpretation.png)

Additional experiements are underway to try different data combinations and different models, such as KPrototypes.


### Presentation
* Presentation - Interactive Maps (sample provided below):

Originally we depicted life expectancy data on html page using JS Leaflet:
* <img width="1329" alt="Screen Shot 2022-12-12 at 8 07 01 PM" src="https://user-images.githubusercontent.com/108832056/207201154-59ead66d-f9a2-4fa8-8aa3-6d891b5f99eb.png">

Now began creating interactive maps in Tableau, which will be the ultimate location of our final dashboard:
<img width="1443" alt="Screen Shot 2022-12-17 at 8 31 31 PM" src="https://user-images.githubusercontent.com/108832056/208272758-dc6e6d47-a09e-4920-8e6c-02df7a8af42b.png">
* Features "Year" slider that will allow user to adjust graphs accordingly for a year of interest between 2000-2019
* Further metrics are to be added as graphs/maps once data is aggregated into GeoJSON file

Further Fleshing Out of Tableau Dashboard to Include Full Life Expectancy Page
Year 2000:
<img width="1443" alt="Screen Shot 2022-12-18 at 12 47 26 AM" src="https://user-images.githubusercontent.com/108832056/208283544-14a8a0ff-8f07-4ebd-959f-8db73505b6d5.png">
Year 2019:
<img width="1463" alt="Screen Shot 2022-12-18 at 12 49 24 AM" src="https://user-images.githubusercontent.com/108832056/208283626-d4957a60-2bfe-47e4-97ef-1cbc588a63b8.png">

Dashboard: Life Expectancy
<img width="1461" alt="Screen Shot 2022-12-19 at 12 03 17 AM" src="https://user-images.githubusercontent.com/108832056/208351564-01afe3ac-fe1e-4ace-bf2a-671d6b665906.png">



### Data Accreditation:

* Life Expectancy: https://data.worldbank.org/indicator/SP.DYN.LE00.IN
* Population: https://www.unfpa.org/data/world-population-dashboard
* GDP: https://data.worldbank.org/indicator/NY.GDP.MKTP.CD?end=2021&start=1960
* Other data: https://databank.worldbank.org/source/world-development-indicators
* ISSA - The International Social Security Association (ISSA) is the world’s leading international organization for social security institutions, government departments and agencies.  The ISSA compiles international country profiles with information about the scope and breadth of each country's social security program(s).  They provided the type of system employed by each of the countries in this study, as well as the definitions of the system types.  Links to the country profiles are included within the `country_profile_urls.csv` file.
