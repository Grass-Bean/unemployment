# **SC1015 Project**

## **Introduction**
This repository contains the codebase for our mini-project. For detailed instructions regarding the project requirements and video presentation guidelines, please refer to the following files:
- [Project Requirements](./proj_req.md)
- [Video Presentation Guidelines](./video_req.md)

## **Project Overview**
### Problem statement:
- Find out if we are overpaying for a car in the second hand market.
### Our approach: 
- Fit some features into an appropriate model to predict the car prices. The model would be able to describe on average what price tag is set on a car with a given set of features.

## **Motivation**
- There are many variables at play when deciding to purchase a second hand car such as seller reputation, car brand, history of usage, etc.
- Using a machine learning model trained on many different types of cars to estimate the price of any second hand car would ease the decision making process.
- We chose a dataset sourced from https://www.kaggle.com/datasets/austinreese/craigslist-carstrucks-data due to the large number of samples to play with, the variety of car models and the richness of its features.

## **Data Preparation and Cleaning**
- Missing data was generally imputed with a new feature that describes the data is missing. Our rationale for this was that people are willing to pay at a different price point if there is missing data due to the risk of incomplete information.
- Categorical data were purely one-hot encoded as a result of the way we imputed data.\
- Textual data proved most challenging where we attempted to clean up urls, punctuations, english stop words. We then proceeded to tokenize and lemmatize them before feeding it into a tfidf vectorizer.
Text with more than 95% frequency and less than 5% frequency were droppped to reduce the number of features generated. Our assumption was that these words would not contribute significantly to the overall meaning of the description and although somewhat handled by a low tfidf value, deleting them would be better in consideration of computation simplicity.
- Distance to nearest city was added as a new feature in consideration of higher demand for vehicles due to a larger population in urban areas.
- Numerical data were scaled using standard scaling to fit them to a similar scale to minimise the effects of their magnitude on loss/error calculation.
- A natural log was also applied where appropriate, such as on prices and odometer readings.

## **Exploratory Data Analysis (EDA)**
- Odometer readings and car age were found to be highly correlated with prices. Which should not be of surprise considering a less used/newer car would be valued more.

## **Machine Learning Techniques**
### We have tested the following models:
- LinearRegressor (benchmark)
- Lasso
- Ridge
- DecisionTree
- XGBoost
- Neural Networks
### Rationale for used models:
- Linear model was purely used as a benchmark for other models due to its simplicity.
- Lasso and Ridge models were used to explore the effects of L1 and L2 regularisation on a Linear model.
- The remaining models were used to try and capture the non-linear relationships between variables in increasing order of complexity.

Note that we didn't explore dimensionality reduction techniques despite the large number of features due to the number of train samples being significantly larger.

## **Model Performance**
Performance of models are judged based on R2 score and mean square error metrics.\
Metrics were obtained using a hold-out validation set.
| Model              | R2 Score | Mean Square Error |
|--------------------|----------|-------------------|
| Linear             | 0.83     | 0.17              |
| Lasso              | 0.00     | 0.99              |
| Ridge              | 0.83     | 0.17              |
| Decision Tree      | 0.81     | 0.19              |
| XGBoost            | 0.90     | 0.10              |
| Fine-tuned XGBoost | 0.93     | 0.07              |
| Neural Network     | 0.88     | 0.12              |
## **Results and Insights**
- Models tend to struggle to predict accurately with incomplete data.
- Model usually predict prices to be below $200,000 indicating bias in the data, more data of higher value cars could have been added to improve model performance.
- A substantial amount of information from description column describes the features in the other columns, extracting these features to impute missing values may have been more appropriate.
- Data is solely from the US market so model is overfitted to US data, it likely cannot generalise well to the used car market outside of the US.

## **Individual Contributions**

- **Member 1**:  
  (Contribution description)

- **Member 2**:  
  (Contribution description)

- **Member 3**:  
  (Contribution description)

## **References**
- Main Dataset: 
   - https://www.kaggle.com/datasets/austinreese/craigslist-carstrucks-data
- Auxillary Dataset(s):
   - https://www.kaggle.com/datasets/sergejnuss/united-states-cities-database 

## **How to Use this Repository**

1. Clone the repository:
   ```bash
   git clone <repository-url>
   ```

2. Navigate to the project directory:
   ```bash
   cd <project-directory>
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Open the notebooks and run them in the following order:
   1) eda_part1.ipynb
   2) eda_part2.ipynb
   3) text.ipynb
   4) models.ipynb
   ```bash
   jupyter notebook notebook_name.ipynb
   ```

## **For More Information**
- For detailed project requirements, please refer to the [Project Requirements](./proj_req.md).
- For video presentation guidelines, please refer to the [Video Presentation Guidelines](./video_req.md).
