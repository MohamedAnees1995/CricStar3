# Retail Sales prediction (Regression)


## Objective
Rossmann operates over 3,000 drug stores in 7 European countries. Currently, Rossmann store managers are tasked with predicting their daily sales for up to six weeks in advance. Store sales are influenced by many factors, including promotions, competition, school and state holidays, seasonality, and locality. With thousands of individual managers predicting sales based on their unique circumstances, the accuracy of results can be quite varied.

 The objective is to predict the "Sales" for each store on the basis of given input features.
## Dataset used

Two datasets are used:

### (1) Rossmann Stores Data.csv 
 The dataset contains historical data including Sales of each Rossmann store across Europe.

```
- Store : a unique Id for each store
- DayOfWeek : Day of week (1-7)
- Date :  Date    
- Sales : the turnover for any given day (DEPENDENT VARIABLE)         
- Customers : the number of customers on a given day  
- Open : an indicator for whether the store was open: 0 = closed, 1 = open         
- Promo : indicates whether a store is running a promo on that day       
- StateHoliday : indicates a state holiday.a = public holiday, b = Easter holiday, c = Christmas, 0 = None
- SchoolHoliday : indicates if the (Store, Date) was affected by the closure of public schools

```

- Total number of rows in data : 1017209
- Total number of columns : 9


### (2) Store.csv

The dataset conatains general information of each store.

```
- Store :   a unique Id for each store                 
- StoreType :                  differentiates between 4 different store models: a, b, c, d 
- Assortment :    describes an assortment level: a = basic, b = extra, c = extended              
- CompetitionDistance :  distance in meters to the nearest competitor store    
- CompetitionOpenSinceMonth :  gives the approximate  month of the time the nearest competitor was opened
- CompetitionOpenSinceYear :  gives the approximate year of the time the nearest competitor was opened            
- Promo2 :   Promo2 is a continuing and consecutive promotion for some stores: 0 = store is not participating, 1 = store is participating                   
- Promo2SinceWeek :  describes the calendar week when the store started participating in Promo2         
- Promo2SinceYear :      describes the year when the store started participating in Promo2      
- PromoInterval :   describes the consecutive intervals Promo2 is started, naming the months the promotion is started anew. E.g. "Feb,May,Aug,Nov" means each round starts in February, May, August, November of any given year for that store         

```

- Total number of rows in data : 1115
- Total number of columns : 10
## Data Cleaning and Feature Engineering

### (1) Removing Duplicate rows
- No duplicate rows were present in dataset.

### (2) Handling null values
- No null values were present in Rossmann dataset.  
- Null values were present in sales dataset.

To remove null values in sales dataset I have imputed them with mode of the respective column.


### (3) Converting columns to appropriate data types

- Changed datatype of `Date` to date type. 

### (5) Creating new columns
- Created new columns `Day`,`Week` and `Month` from date column.


### (6) Feature encoding
- Used One hot encoding to transform categorical feature - `StoreType`, `Assortment`, `PromoInterval`.
- Used Label encoding to transform categorical features - `StateHoliday`.

### (7) Handling skewness
- Used square root transformation and logarithmic transformation to reduce skewness of skewed features.

### (8) Removing outliers
- Checked for outliers in sales column using IQR method and dropped them.

### (8) Standardization of features
- Used `Min-Max Scaler` for normalization of features.This step scales data into a uniform format that would utilize the data in a better way while performing fitting and applying different algorithms to it. 

## Exploratory Data Analysis

Mainly performed using Matplotlib and Seaborn library and the following graph and plots had been used:
  - Bar Plot.
  - Histogram.
  - Scatter Plot.
  - Pie Chart.
  - Line Plot.
  - Heatmap.
  - Box Plot
  - Violin plot
             


- Sales were almost consistent in each year.
- Sales increased slighlty at the end of the year.
- Sales decreased on state holidays as compared to non holiday.
- School holidays didnt impacted sales of stores.
- Promotions increased sales of stores significantly.
- Store type 'a' has higher sales as compared to other types of stores.
- Store with extra assortment level has higher sales as compared to basic and extended level.


## Model Building


Since we have to predict the sales of the stores, so this is a regression problem. Based on the problem statement  I decided to develop predictive models using following algorithms and have compared there performance.
```

- Random Forest
- Linear Regression
- Lasso
- Ridge
- Elastic Net


Following necessary steps have been employed for better model performance.
                (i)   train test split for model evaluation.
                (ii)  Hyperparameter tuning for best learning parameters that developed a better model. Hyperparameter tuning was done with the help
                      of GridSearchCV.
                      
                      
                  
```


### Evaluation metrics

To evaluate the models I have used adjusted R2-Score.


## Conclusion

```
                 (i)  The initial phase of the project involved thorough data
exploration and cleaning. We identified and addressed missing values, particularly in columns such as 'CompetitionDistance', 'CompetitionOpenSinceMonth', 'CompetitionOpenSinceYear', 'Promo2SinceWeek', 'Promo2SinceYear', and 'PromoInterval'. For the 'Sales' column, it was observed that 172,817 entries had zero sales. To mitigate this, a new DataFrame was created by removing rows with zero sales, setting the stage for a more focused and accurate analysis.

Several data type conversions were performed to optimize the dataset for machine learning algorithms. Categorical columns, including 'StateHoliday', 'Assortment', and 'StoreType', were transformed from 'object' to 'int'. This process involved mapping different string values to corresponding integer representations, facilitating a numerical input for machine learning models.

To enhance the predictive power of the model, additional features were engineered. The 'Date' column was converted to 'datetime' format, and a new column was created to extract the month values. This not only improved the temporal aspect of the data but also allowed the model to capture potential seasonality trends in retail sales.

Various machine learning algorithms were applied to the preprocessed and engineered dataset. These algorithms included but were not limited to regression models, decision trees, and ensemble methods. The model training process aimed to predict retail sales accurately based on historical data and engineered features.

After extensive training and validation, the models were evaluated using standard metrics. The accuracy score emerged as a crucial metric, and the models collectively achieved an accuracy rate of around 74%. This performance indicated the effectiveness of the selected algorithms and the significance of the preprocessing steps in creating a refined and reliable predictive model.

The Retail Sales Prediction project successfully addressed data challenges, optimized features, and trained models to forecast sales with a commendable accuracy rate. However, the project is an iterative process, and there are opportunities for further enhancement. Future directions could include exploring more sophisticated algorithms, incorporating external factors like economic indicators or weather data, and conducting a more granular analysis to capture store-specific trends.

In conclusion, the Retail Sales Prediction project not only provided valuable insights into the dynamics of retail sales but also demonstrated the importance of thoughtful data preprocessing, feature engineering, and model selection in achieving accurate predictions. The outcomes of this project can potentially empower retailers with better decision-making capabilities, optimizing inventory management and overall business strategies.
                         
                 (ii)  Linear Regression also performed fairly well.
                         adjusted R2-Score for test dataset = 0.87
                         
                          
                 
           

```

