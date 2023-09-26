![image](https://github.com/matiasortizluna/chicago-crimes/assets/64530615/e26de271-308c-4196-a86b-721268456682)![image](https://github.com/matiasortizluna/chicago-crimes/assets/64530615/ba27b176-4efc-4d99-af60-92ece0f8420f)# Welcome to chicago-crimes repository

Computer Science Master's degree “Data Mining II" subject project: Analysis of data of crimes in Chicago made in R.
By Matias Luna, Inês Gonçalves, Ana Torres & Emma Romdhane.

# About the project
For this assignment, we were provided with the Chicago Crimes dataset, a widely recognized and comprehensive col- lection of crime data, encompassing various offense categories, geographic information, and temporal details which covers the years 2017 to 2023.
This project has two goals. The first one is to explore the dataset using visualizations, association rules, recommen- dations and link analysis. The second one is to build four machine learning models capable of predicting the occurrence of crimes (or specific characteristics associated with them).

# Data Pre-Processing

The first thing we did was pre-processing the data, which included the following tasks:

- Removed rows with missing values

- Merged duplicated types: CRIM SEXUAL ASSAULT and CRIMINAL SEXUAL ASSAULT

- Performed Feature Engineering:
    Date -> YearMonth, Year, Month, Day, Hour
    Date -> WeekDay
    Date, Updated On -> UpdateDays
    Month -> Season
    Hour -> Nightime
    Hour -> TimeOfDay

Then, we focused on the data from the years between 2017 and 2022 to perform the analysis and train the model, and the crimes of 2023 to be tested on.

# Exploratory Data Analysis

We used ggplot2 to produce the visualizations. The first thing we decided to analyse was the evolution of the Chicago crimes through time.

It is clear the influence of the COVID-19 pandemic on crime rates, as we can see a drop in crime in April 2020 and February 2022, which correspond to periods of time where Stay-At- Home Executive or Advisory Orders were in place, as well as Cessation of Alcoholic Liquor Sales.

![image](https://github.com/matiasortizluna/chicago-crimes/assets/64530615/e1eb8b3e-a9e6-4299-b77c-de119cadad32)

We decided to investigate these evolution per primary type, and we found interesting patterns on DECEPTIVE PRAC- TICE, NARCOTICS and MOTOR VEHICLE THEFT.

![image](https://github.com/matiasortizluna/chicago-crimes/assets/64530615/ede68f61-8005-45d6-8513-7823bcbefdc6)

We can see that Narcotics crimes drop after COVID-19 and have stayed this way. Deceptive Practice was abnormally high during October 2020 and April 2021. The rise of Motor Vehicle Theft since July 2022 could perhaps be explained by a TikTok challenge promoting the theft of cars of the brands Kia and Hyundai.

We then investigated primary type of crime per Chicago ward. We chose to show only the 10 most significant types. As it can be observed, ward 42 has the bigger number of crimes, which can be explained by the fact that this ward is Chicago’s Central Business District.

![image](https://github.com/matiasortizluna/chicago-crimes/assets/64530615/7816a607-632b-4bef-9350-d782924955f4)

Most of the crimes occur during the night (from 8pm to 6am). During the rest of the day parts, the crimes are relatively proportional. During these times there is not a type of crime that stands out. This can be seen in the figure below.

![image](https://github.com/matiasortizluna/chicago-crimes/assets/64530615/a225710f-7a06-4590-b5ab-cc8a02af47b8)

As it is observable in the graph below, most of the crimes occur during the Summer followed by Autumn, which can be due to a higher number of tourists during the vacations season.

![image](https://github.com/matiasortizluna/chicago-crimes/assets/64530615/98ac552d-66d6-4a92-861b-a76e5aead3dd)

# Modelling

To ensure data quality, we performed data cleaning by removing NAs and irrelevant features. Unique identifiers like ’ID’ and ’case number’ were excluded to prevent overfitting and redundancy. Additionally, date-type columns were omited, although we re-used them as individual components. An initial RF execution was made to identify the features that have the most importance, and sadly, columns like ’Block’, ’IUCR’, ’Description’, and ’Location Description’ were considered among the most significant but couldn’t be included due to their large number of unique values and limited computational resources.

The selected features for the models included the FBI Code, Primary Type, Community Area, and variables representing police geographic area, district, and ward. We also incor- porated date-related variables, such as year, hour, weekday,month, nighttime, time of day, and season. Instead of using the ’Block’ column, we utilized latitude and longitude to capture crime locations. Additionally, we retained the ’Do- mestic’ column, as well as the target variable ’Arrest’ for our classification problem.

To ensure compatibility with machine learning models, we converted data types to factors or numeric. We also used data augmentation to address the class imbalance of the arrest variable, because the original proportion of the minority class (TRUE) was lower (17%); this process allows models to have a 0.5 probability for each class.

The dataset was divided into training and testing subsets with a 70-30 split. We employed four ML approaches: logistic regression, CART, random forests, and Naive Bayes. Each model was trained on the prepared dataset and evaluated using the testing data.

The performance of each model was assessed using various metrics. On the following figure it is compared them by plotting a ROC Curve of the four models.

![roc_various](https://github.com/matiasortizluna/chicago-crimes/assets/64530615/aff6810f-506b-471a-a573-f4e6bcc3abd5)

Additionally, a feature importance analysis was conducted to identify the most influential variables in the models.

![image](https://github.com/matiasortizluna/chicago-crimes/assets/64530615/87be8788-4969-4a6a-b2d3-497a427fa9b3)

The results indicated that all models demonstrated promis- ing predictive performance. The Random Forest model achieved the highest performance with a ROC value of 0,9834. These results provide valuable insights for law enforcement agencies in developing better crime prevention strategies.

# CONCLUSION

Although models with different feature combinations and dataset dimensions were tested, satisfactory results within a reasonable time frame were not achieved.

Future research could focus on improving model perfor- mance and exploring more advanced ML techniques for more accurate crime prediction models.
















