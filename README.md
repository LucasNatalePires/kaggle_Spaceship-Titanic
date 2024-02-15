**The goal is to prevent passengers from being transported to an alternate dimension. The dataset is available in the repository or you can view it in the project notebook.**


In this code, you will find:

Data treatment, including null data:
  - The following functions were used:
    - [mean](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.mean.html): Calculates the average of the values. was used in the columns in which the values ​​represented the financial value spent per customer, on the various extra services
      
    - [median](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.median.html): Calculates the median of the values ​​(average value of the set, sorted in ascending order). It was used to complete the 'Age' column, as it makes more sense than taking the average of all ages
    
    - [mode](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.mode.html):Returns the value that appears most in the set. It was used in columns where there were few options, so I assumed that most people were included in this trend.


Data in which the variable type was of a type not compatible with the algorithm used:

  - Use of the [OneHotEncoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html):
  Convert classes to categories by transforming them into numeric values, 1 or 0, if it presents the condition
      
  - Application of functions created, from def func(): Creation of a simple function that assigns the value 0 or 1 to Boolean variables
   
  - [LabelEncoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html): 
    Converts categorical classes by transforming them into numeric values. It was used in situations where there are many options, making the use of OneHotEncoder longer to process, more cumbersome (more data would be created) and the DataFrame is less clear. This all interferes with our accuracy.

  - Creation of 3 new columns, from an existing one, using [str split()]():
    The column with 'Cabin' information was confusing, mixing deck, number, side. Using str.split(), I created new columns from the 'Cabin', with the most visual and straightforward information.


    
Graphs were built to make the dataFrame more visual and easier to interpret, the following were used:

  - [matplotlib](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.subplots.html#matplotlib.pyplot.subplots): library responsible for manipulating graphics
  - [sea born](https://seaborn.pydata.org/api.html): It allowed generating a heatmap to look for any correlation between the variables
  - [Standart Scaler](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html): Used to standardize features by removing the mean and scaling to unit variance.




In terms of machine learning:

  - [Random Forest](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)
  - [Logistic Regression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)
  - [MLP-Classifier](https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPClassifier.html)


  
[accuracy_score](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.accuracy_score.html) and [confusion_matrix](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.confusion_matrix.html) were used to check the accuracy value and the matrix with errors/hits
