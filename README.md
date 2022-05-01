# Data Analysis_Happiness
Data Analysis on the Most Significant Factor of Happiness Around the Globe

### Introduction
With the advent of Covid-19 over the past few years, the devastation of the pandemic such as
millions of deaths, economic strife and unprecedented restrictions on social interaction has
significantly affected people's mental health. Researchers and scientists worldwide have been
analyzing the impact of this despair and uncertainty and claim that "the deterioration in mental
health could linger long after the pandemic has subsided" (Nature News). As the world is
progressing day by day, our focus tends to shift toward endless developments rather than
focusing on certain characteristics that actually matter daily, such as overlooking happiness.
While the research claims that the current mental health status could linger long after the
pandemic, it is significant to understand the determining factors of happiness and how they affect
the well-being of individuals. Thus, as a society, people can focus on certain factors together to
form a happier environment. The "World's Happiness Report 2021" data from Kaggle was
utilized for analysis. The data consists of 149 inputs of countries and happiness score estimates
in six factors - economic production, social support, life expectancy, freedom, absence of
corruption, and generosity in each country around the world. Through this research and data
analysis, we will ascertain the answer to the question of "What are the most significant factors of
happiness all over the globe?" to contribute a positive impact of particular control measures on
changes in people's well-being and to appraise the management of future pandemics.
### Methods

The analysis will follow the following procedure in order: data cleaning and transformation,
exploratory data analysis, training and test sets, model proposal, model selection and diagnostics,
and model validation. The data cleaning includes replacing the column names with proper names
to make the data analysis process easier. During the exploratory data analysis, we checked the
null values and categorical values as well as the density and distributions of continuous
variables. Then, we plotted the histogram and check the p-value to investigate the outcome and
whether it is normally distributed. In order to build training and test sets, we split the data into a
7:3 ratio. After setting the test models, we proceed to move forward for variable selections using
forward, backward, and stepwise selection and evaluated the most appropriate selection variables
by building and comparing each model. Then, we will investigate multicollinearity and variance
inflation factor (VIF) between the predictors of the model and resolve it if there exist many
multicollinearities by removing certain variables from the selection model. Each model will be
examined by checking normality, constant variance, homoscedasticity, and outliers to select the
best fit model. Furthermore, we will compute the AIC of the fit model and adjust R-squared to
finalize the model. With this final model, we evaluate the most significant factor to increase
happiness scores and predict other countries’ happiness scores using the current existing dataset.
To evaluate the model performance, root mean squared error (RMSE) was used to examine
whether the model is robust depending on the RMSE value.

### Results
[Data Transformation and Exploratory Data Analysis]
<img width="835" alt="image" src="https://user-images.githubusercontent.com/60108438/166161416-9cc7f16e-1931-42e0-ae35-4e696f5034f9.png">

To begin with the data cleaning and transformation process, the column names were replaced
with proper names. Through the Exploratory Data Analysis (EDA), we figured that there exist 2
categorical and 18 continuous variables in the dataset that contains 149 countries (Figure 1, 3).
There were no missing values and 0 duplicate countries in the dataset (Figure 2).

<img width="913" alt="image" src="https://user-images.githubusercontent.com/60108438/166161435-3c7f38b1-f857-40b9-93f7-310cbc24b59f.png">

<img width="642" alt="Screen Shot 2022-05-02 at 4 25 33 AM" src="https://user-images.githubusercontent.com/60108438/166161458-7e7ee79a-c6f2-48aa-a776-6b90e4afc58b.png">

According to the histogram of the ladder score, as the p-value > 0.05, the outcome is normally
distributed.

### Model Selection
In order to fit the best model, we built training and test sets by splitting the data into a 7:3 ratio.
Then, we build forward selection, backward selection, and stepwise selection models. For the
forward selection model, the variables that were chosen were "lower whisker", "upper whisker",
and "Dystopia_residual". For backward selection, "upper whisker", "lower whisker",
"Logged_GDP_per_capita", "Healthy_life_expectancy", "Generosity",
"Explained_by_Social_support", "Explained_by_Freedom_to_make_life_choices",
"Explained_by_Perceptions_of_corruption", "Dystopia_residual” were chosen. Then, we built a
hybrid stepwise selection model and investigated that it indicates the same results as the forward
selection variables. The model summaries below prove the same results.

<img width="494" alt="image" src="https://user-images.githubusercontent.com/60108438/166161486-f2fff6a0-186b-4a92-9357-97279011dc5a.png">
<img width="494" alt="image" src="https://user-images.githubusercontent.com/60108438/166161504-25dc5ace-155c-46b7-9fc2-665cb8496edd.png">
<img width="565" alt="image" src="https://user-images.githubusercontent.com/60108438/166161510-74203e38-df51-4fab-965f-c5fd07bdcb49.png">

### Model Improvement and Assumption Check
As the stepwise selection method is the same as the forward selection, now we train and compare
two models: forward vs. backward selection models.

Then, we check for multicollinearity and variance inflation factor (VIF) of the model. After
fitting the forward selection model, we know that either the lower whisker or upper whisker
should be removed from the model and be refitted. After fitting the backward selection model,
we figure that too much multicollinearity exists in the model between predictors, thus this is not
the best model. To resolve multicollinearity, upperwhisker was removed from the forward
selection model. In addition, upperwhisker and lowerwhisker were removed from the backward
selection model. Thus, all the VIF of the predictors for each model was less than 10.

### Model Diagnostics
The model will be examined by checking normality, constant variance (homoskedasticity), and
outliers. For the forward selection model, although the normality assumption was not satisfied,
the constant variance assumption was met. For the backward selection model, both normality
assumption and constant variance assumption were satisfied well. However, it would be better if
we exclude the Rwanda observation from the analysis.

<img width="580" alt="image" src="https://user-images.githubusercontent.com/60108438/166161546-3435b0dc-2c36-436c-9776-04df8f8f3a81.png">

<img width="635" alt="Screen Shot 2022-05-02 at 4 28 19 AM" src="https://user-images.githubusercontent.com/60108438/166161556-26b916c4-2f34-407d-8f79-6d1f5252b521.png">

As Backward’s AIC is lower than that of the Forward and Backward's adjusted R-squared is
greater than that of Forward2, our final model is "Ladder_score ~ Logged_GDP_per_capita +
Healthy_life_expectancy + Generosity + Explained_by_Social_support +
Explained_by_Freedom_to_make_life_choices + Explained_by_Perceptions_of_corruption +
Dystopia_residual."


<img width="613" alt="Screen Shot 2022-05-02 at 4 28 46 AM" src="https://user-images.githubusercontent.com/60108438/166161570-e460cd17-4e17-421b-86ab-54f80fb5ecfd.png">

### Model Validation
The actual ladder score of the countries in the test set was compared to the predicted ladder score
by the trained final model. To evaluate the model performance, root mean squared error (RMSE)
was used. As RMSE = 0.0008242059, which is very small, we can say that the final model is
robust.

<img width="786" alt="Screen Shot 2022-05-02 at 4 29 16 AM" src="https://user-images.githubusercontent.com/60108438/166161593-1f283aff-dc9a-4eea-918d-9f395ff96a32.png">

### Discussion
According to our final model and results, the data claims that the most significant factor to
increase happiness scores is the perception of corruption. Since how the citizen perceive the
culture of the society and its perspective of the political circumstance happening in the world, it
indicates that the transparency of communicating the real news to the citizen is crucial to have
trust.
