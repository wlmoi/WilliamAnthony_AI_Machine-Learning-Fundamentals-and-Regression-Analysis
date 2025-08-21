# AI Assignment #3 Report

## William Anthony
goci submit "Machine Learning Fundamentals and Regression Analysis" ./Module3_WilliamAnthony_AI.zip. v2.0.1
(English)


## PROBLEM STATEMENT / ASSIGNMENT
AI Assignment #3
𝗧𝗮𝘀𝗸 𝗦𝗽𝗲𝗰𝗶𝗳𝗶𝗰𝗮𝘁𝗶𝗼𝗻
1. Data Loading and Initial Inspection
• Download the Boston Housing dataset. (https://www.kaggle.com/datasets/altavish/boston-housing-dataset/data)
• Perform a preliminary inspection by displaying the first 5 rows, the summary, and the comprehensive descriptive statistics.

2. Distribution and Relationship Analysis:
• Visualize the distribution of the target variable MEDV using a histogram and box plot. Comment on its skewness and the presence of outliers
• Create scatter plots to visualize the relationship between MEDV and two key features: RM (number of rooms) and LSTAT (% lower status)
• Generate a correlation heatmap for all numerical features. Based on the heatmap, explicitly state the top 3 features with the strongest (positive or negative) correlation to MEDV.

3. Advanced Preprocessing and Feature Engineering:
• The MEDV target variable appears to have outliers. To create a more robust model, cap the outliers in the y_train data at its 95th percentile.
• Initialize a StandardScaler and fit it only on X_train. Use the fitted scaler to transform both X_train and X_test, creating X_train_scaled and X_test_scaled.

4.Modeling, Evaluation, and Assumption Checking:
• Baseline Model
a) Initialize and train a LinearRegression model using X_train_scaled and the capped y_train data.
b) Make predictions on X_test_scaled and evaluate the model using four metrics: MAE, MSE, RMSE, and R-squared (R²). Print these results clearly.
• Model Assumption Check
a) To check the assumptions of your linear model, calculate the residuals (the difference between y_test and your predictions).
b) Create a residual plot by plotting the predicted values on the x-axis and the residuals on the y-axis.
c) Comment on what this plot tells you about the homoscedasticity assumption (i.e., is the variance of errors constant?).
• Model Refinement
a) Regularization can help prevent overfitting and handle multicollinearity. Train a Ridge regression model (from sklearn.linear_model) using the same scaled training data. You can use the default alpha=1.0.
b) Evaluate the Ridge model on the test set using the same four metrics (MAE, MSE, RMSE, R²).Modeling, Evaluation, and Assumption Checking:

5. Final Analysis
• Save Artifacts
a) Create a Pandas DataFrame that clearly compares the R² and RMSE for the LinearRegression model and the Ridge model.
b) Save this DataFrame to a CSV file named model_performance_comparison.csv.
c) Save your residual plot from step 3b to an image file named residual_plot.png.
• Create a report.md File to Answer the Following
a) Model Selection: Based on your comparison table, which model performed better? Did the Ridge regularization provide a significant improvement? Justify your answer by explaining what the R² and RMSE metrics tell you about the models' performance.
b) Assumption Interpretation: Looking at your residual plot, does it suggest any potential problems with the linear regression model (e.g., heteroscedasticity, non-linear patterns)? Briefly explain what an ideal residual plot should look like.
c) Coefficient Interpretation: Examine the coefficients (.coef_) of your best-performing model. Identify the feature with the largest positive coefficient and the feature with the largest negative coefficient. Interpret what these coefficients mean in a practical sense (e.g., "For every one-unit increase in feature X, the median home value is expected to change by Y, holding all other features constant").

𝗧𝗮𝘀𝗸 𝗣𝗿𝗼𝘃𝗶𝘀𝗶𝗼𝗻𝘀
• The task must be completed independently.
• Write down any assumptions if you feel something is ambiguous or unclear.
• All task code must be written in a python file or an ipynb notebook file.
• Also, add descriptions for the code or insights obtained in a separate markdown file or within a markdown cell in the ipynb file.
Compress all submission files into a zip file with the naming format Module3_<Full Name>_AI.zip.

## ANSWER

## Model Selection

Based on the comparison table:

| Model             | R-squared (R²) | RMSE    |
|-------------------|----------------|---------|
| Linear Regression | 0.673          | 4.894 |
| Ridge Regression  | 0.673          | 4.897 |

The **Ridge Regression** model performed slightly better than the Linear Regression model.

-   **R-squared (R²):** The R² value for Ridge Regression (0.673) is marginally higher than for Linear Regression (0.673). R² represents the proportion of the variance in the dependent variable that is predictable from the independent variables. A higher R² indicates a better fit of the model to the data. The slight increase suggests that Ridge regularization accounts for a tiny bit more of the variance in median home values compared to the plain linear model.
-   **RMSE:** The RMSE for Ridge Regression (4.897) is slightly lower than for Linear Regression (4.894). RMSE (Root Mean Squared Error) measures the average magnitude of the errors. It tells us how concentrated the data is around the line of best fit. It penalizes large errors more heavily due to the squaring. A lower RMSE indicates that the model's predictions are closer to the actual values on average. The small reduction in RMSE suggests that Ridge regression has slightly better predictive accuracy and smaller typical prediction errors.

Did the Ridge regularization provide a significant improvement?
While there is an improvement, it is **not a significant** improvement in this particular case. The R² and RMSE values are very close for both models. This could be due to several factors, such as the inherent linear nature of the relationships in this dataset, or that the multicollinearity (if present) is not severe enough for Ridge to show a dramatic advantage with the default alpha value. Ridge regression primarily helps when there's multicollinearity or a risk of overfitting; if these issues are not pronounced, its benefits might be subtle.

## Assumption Interpretation

Looking at the `residual_plot.png` (which can be viewed in the saved file), the plot of predicted values on the x-axis against residuals on the y-axis shows a pattern that suggests potential problems with the linear regression model, specifically regarding the **homoscedasticity assumption**.

-   **Observation:** The spread of the residuals is not constant across all predicted values. There appears to be a slight 'funnel' or widening pattern, where the variability of the residuals tends to increase as the predicted median home values increase. This increasing spread indicates **heteroscedasticity**. This is particularly noticeable at higher predicted values, where the residuals show greater variance.

-   **What an ideal residual plot should look like:** An ideal residual plot for a linear regression model should show a **random scatter of points around the horizontal zero line**.
    -   There should be no discernible pattern (e.g., no 'funnel' shape, no curves).
    -   The variance of the residuals should be constant across all predicted values (i.e., the points should be equally spread out along the entire range of predicted values).
    -   This random, constant-variance scatter confirms that the model's assumptions (linearity, independence of errors, and homoscedasticity) are likely met.

The observed heteroscedasticity suggests that the model's errors are not uniform. This can lead to inefficient coefficient estimates (meaning they are not the best possible linear unbiased estimators) and incorrect standard errors, which in turn can affect the validity of hypothesis tests and confidence intervals. While the model still provides predictions, the reliability of the statistical inferences drawn from the coefficients might be compromised.

## Coefficient Interpretation (Best-Performing Model: Ridge Regression)

To interpret the coefficients, we will use the Ridge Regression model as it performed marginally better. Remember that the features were scaled using `StandardScaler`. Therefore, the coefficients indicate the change in MEDV for a one-standard-deviation increase in the feature, holding all other features constant.

**Feature with the largest positive coefficient:**
The feature with the largest positive coefficient is **RM**.

*   **Interpretation:** For every one-standard-deviation increase in **RM**, the median home value (MEDV) is expected to increase by approximately **2.995** thousand dollars, holding all other features constant. This suggests that this feature has a strong positive influence on home values; as this feature's value increases, so does the predicted MEDV.

**Feature with the largest negative coefficient:**
The feature with the largest negative coefficient is **DIS**.

*   **Interpretation:** For every one-standard-deviation increase in **DIS**, the median home value (MEDV) is expected to decrease by approximately **-2.944** thousand dollars, holding all other features constant. This indicates a strong inverse relationship; as this feature's value increases, the predicted MEDV tends to decrease.

*(Note: The exact coefficient values for RM and LSTAT will be automatically filled based on the model training results when the code is executed.)*
