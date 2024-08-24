# PWC_Call_Centre_Trends

## Objective
The call center manager wants insights and transparency into the data available at the call center.

### Requested KPIs
-Overall customer satisfaction
-Overall calls answered/abandoned
-Calls by time
-Average speed of answer
-Agent’s performance quadrant -> average handle time (talk duration) vs calls answered.


## Data Source
The data is given by Pwc Switzerland.

## Tools & Technologies
Excel: For initial data exploration and preparation.
Power BI: To transform data, create interactive dashboards and visualizations.

## Process Overview
### 1. Get the Data
- The dataset is obtained from the Pwc Switzerland.

### 2. Explore the Data in Excel, in this stage, the data is being explored, and after closely examining the dataset, the following points were observed:
- **Data Exploration:** Initial exploration of the dataset to understand its structure and identify necessary columns for analysis. 
    After exploring the data, it is found that is already cleaned but need to change some column name, change data type and need to add calculated column. This small changes will be perform in Power BI.

### 3. Visualize the data in Power BI

Before creating visualizations, we need to transform the data in the Power Query Editor as well as need to add some calculated columns:

1. **Transform Data**:
   - In this stage, we have changed the name of some columns and corrected their data type.
   - Calculated columns are created, In_Seconds and Hours columns are added br creating DAX measures.


### Visualizations
Now coming on to Visualizations, we have used:
Clustered Column Chart, Scatter Chart, Pie Chart, Stacked Bar Chart & Cards

#### 1. Clustered Column Chart

This visualization shows total call answered and abandoned

#### 2. Scatter Chart

This chart shows a relation between agents total call answered vs their Performance Quadrant.

#### 3. Pie Chart

This chart shows the total proportion of calls by their topic.


#### 4. Stacked Bar Chart

This chart represents the total no of calls by their time.

#### 5. Cards

The cards are used to display Overall customer catisfaction, Avg speed of answer, Agents's performance quadrant, Count of calls answered/abandoned and isuues resolved/not resolved.These cards provide quick insights.

![Screenshot (235)](https://github.com/user-attachments/assets/d1a287cc-2304-4efc-91cd-f8ceb551f46b)

## DAX Measures

### 1. Agent’s Performance Quadrant
```sql
Agent’s Performance Quadrant = 
CALCULATE(AVERAGEX(
    'Call_Center',
    (Call_Center[In_Seconds])
),
Call_Center[Answered (Y/N)]="Y")

```

### 2. Average Satisfaction Rating
```sql
Average Satisfaction Rating = CALCULATE(AVERAGE(Call_Center[Satisfaction_Rating]), Call_Center[Answered (Y/N)]="Y")

```

### 3. Average Speed of Answer
```sql
Average Speed of Answer = CALCULATE(AVERAGE(Call_Center[Speed_of_Answers (S)]), Call_Center[Answered (Y/N)]="Y")

```

### 4. Call Count by Hour
```sql
Call Count by Hour = 
COUNTROWS(
    FILTER(
        'Call_Center',
        'Call_Center'[Hour] = SELECTEDVALUE('Call_Center'[Hour])
    )
)

```

### 5. Count of Calls Abandoned
```sql
Count of Calls Abandoned = COUNTROWS(FILTER('Call_Center', Call_Center[Answered (Y/N)] = "N"))
 
```

### 6. Count of Calls Answered
```sql
Count of Calls Answered = COUNTROWS(FILTER('Call_Center', Call_Center[Answered (Y/N)] = "Y"))

```

### 7. Issue Not Resoved
```sql
Issue Not Resoved = COUNTROWS(FILTER('Call_Center', Call_Center[Resolved] = "N"))

```

### 8. Issue Resoved
```sql
Issue Resoved = COUNTROWS(FILTER('Call_Center', Call_Center[Resolved] = "Y"))

```

### 8. In_Seconds
```sql
In_Seconds = 
HOUR([Talk_Duration]) * 3600 + 
MINUTE([Talk_Duration]) * 60 + 
SECOND([Talk_Duration])

```

### 5. Conclusions from the Analysis

Based on the data, here are some insights and findings that can be derived using the visualizations from Power BI:

#### Average speed is **67.52 Seconds**.

#### **3646** issues are resolved and **1354** issues are not resolved.

#### Overall Customer Satisfaction **3.40**.

#### Counts of call answered are **4054**.

#### Counts of call abandoned are **946**.

#### Count of calls by topic.
-1022 calls are related “Streaming” topic.
-1019 calls are related “Technical Support” topic.
-1007 calls are related “Payment Related” topic.
-976 calls are related “Admin Support” topic.
-976 calls are related “Contact Related” topic.


#### Jim has answered maximum no of calls i.e. **536** calls with an avg speed of **66.34 seconds**.
