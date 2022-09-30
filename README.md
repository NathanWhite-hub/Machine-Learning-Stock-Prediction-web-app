# Machine Learning Stock Prediction web-app
This was completed as apart of my WGU Capstone project for my Computer Science Bachelor's for a fictional company I created called HedgeVision.

## Project Purpose
This project’s main purpose was to develop and deliver a model capable of analyzing the NASDAQ for a given company. A secondary purpose of this project was to deliver a dashboard that provided in depth metrics for model performance, market analysis, and virtual testing environment. Through this virtual testing environment potential return on investment was provided in the form of percentage lost or gained. This potential return is also compared against the actual market return percentage. A continual data stream with Yahoo Finance was established for the purpose of continued use and model testing.

![Dashboard View](https://i.imgur.com/2xiMT2i.png)
*Dashboard view of the deployed Jupyter Notebook*

## Dataset
The datasets utilized in this project are provided from Yahoo Finance’s API  and the yfinance library. The Yahoo Finance API provides up to date information on the investment market and can provide data on every company listed on the NASDAQ. This data can be gathered by sending a request to the Yahoo Finance API, to which it will respond with the requested data. The data is presented with the daily open, high, low, close, volume, dividends, and stock splits for the requested time span, in this case of this project, the maximum time the company has been listed, in some cases since the early 1980s. For this project, the dividends and stock splits were not considered significant enough to include as features and are removed during the cleaning process.
 
![Data example](https://i.imgur.com/ga4UG1V.png)
*An example of the raw data for Tesla returned by Yahoo Finance*

The data is thoroughly cleaned, and features are created from the given data. These features include the given open, high, low, close, and volume, as well as weekly, quarterly, annual, annual weekly, and annual quarterly means. In addition, the weekly trend, open close, high close, and low close ratios are added as features. These features assist the model in better understanding the differing data points and allow the model to be more accurate in its classification of data points.

## Data Product Code
The overall code was designed in a module format to better serve the dashboard and can be broken down into four separate modules. The first module handles importing of libraries that the code will use; this is followed the dashboard functions. These functions within here are called by the dashboard module for various user functionalities. Within the module are sub sections that can be separated into the categories of data gathering and preparation, model creation and back testing, and metrics. 

The data gathering subsection is the first subsection called by the dashboard, and it begins by requesting the NASDAQ trading data that was indicated by the user. The next step is data preparation where the data gathered in the previous step is prepared. The data is given a new column named “Target” where a 1 or 0 is assigned to each row based on whether the close price of that row went up or down with 1 being up and 0 down. After the data is returned, the next step is to create features from the data. The main features of close, volume, open, high, and low are added as those features already exist. However, the features of weekly, quarterly, annual, annual weekly, and annual quarterly means as well as the weekly trend, open close, high close, and low close ratios are calculated and added.

After all the features are created and added to the dataset, the next sub section begins. Here, a Random Forest Classifier model is initialized and returned. Next, the training and back testing section begins with taking the prepared dataset from the last sub section and breaking it into a separate training and testing datasets. This allows for proper testing later in this function as the test is conducted on the testing dataset which the model has not been trained on and has not seen prior. After this, the Random Forest model is trained or “fitted” on the training data. The now trained Random Forest model then predicts outcomes of the various datapoints inside the testing dataset. These predictions are documented in the form of 1s or 0s and returned with the actual target values (also 1s or 0s). Both the predicted values and the target values are used for the next sub section, the metrics.

The metrics sub section begins with computing the return (profit) of the back tested data for a year from the day the test was conducted. This return is computed by getting the logarithm of the daily closing price as a percentage change from the prior day. The actual return from the model’s predictions is calculated by taking each prediction and multiplying it by the return calculated just prior to this. Both returns are calculated as a percentage and returned for plotting.

The two returns (the actual returns and the model’s returns) are then plotted against each other and displayed over the year period as a line graph. Text outputs are then sent to the user to tell the user if the model performed better or worse than market. Another line graph is calculated with the overall historical price of the user selected company. From here, two graphs are created; a bar chart to display the total number of each prediction class, and a confusion matrix with data of both the prediction classes and the actual data. Both graphs server to better illustrate the choices that the model made and compare them against the true data.

The bar chart is output with two columns, the number of 0s and the number of 1s, both making up the total amount of model predictions. The second graph, the confusion matrix, outputs the number of choices, both 0s and 1s, and compares it against the true values for 0 and 1. Each portion of the matrix is presented as a heatmap to better illustrate where the model may be skewed and the overall accuracy in a visual format. This then ends marks the last sub section of the second module.

The next and third module holds the code that makes up the dashboard functionality and design. Here, formatting, logos, and the overall functionality is handled. The other modules and overall functionality of the program rely on the use of this module as each function in the previous module is called from here. The next module begins the program by assigning the widgets in the previous module and displaying the dashboard. This can essentially be considered the “main()” entry point for the program

## Effective Visualizations and Reporting
One of the main goals of the project was to provide the user with an interactive and informative dashboard. This was done through responsive design, metrics, and a dynamic design for a plug and play environment. Once the model testing button has been clicked, the data gathering, preparation, and model testing and training process begins. Once the pipeline finishes, the various metrics and model information are output and displayed to the user. The model begins by telling the user the overall models predictions on the entire testing dataset and the precision score of the model.

![Metric Example](https://i.imgur.com/xo8tyAt.png)

*Output text from the program displaying the accuracy and testing dataset predictions*

From here, a graph displaying the historical closing price of the company for the entire dataset is displayed for the user to better visualize how the company has done from its inception. This data can also be used to better interpret the model’s return, as if the company has done poorly, it is unlikely the model would see a large return. This graph will change day to day as the daily data from Yahoo finance is updated.

![Metric Example 2](https://i.imgur.com/1e7y3Gs.png)

5 (The historical closing price of Apple that is displayed to the user)


The user is then presented with text displaying what the overall percentage return was in the actual data and what the overall percentage return was for the model’s predictions. This is essentially translated to the model’s profits. Another text line is put out which will state whether the model performed better than the market or worse depending on the two percentage returns. A graph is plotted over the course of a year with two lines: one for the market’s return and one for the model’s return. This shows a timeline of the model trading, and at which point in times it would have made a return.

![Metric Example 3](https://i.imgur.com/v6QX1cS.png)

6 (Output text and graph describing and displaying the model returns)

## Accuracy Analysis
The overall accuracy of the model is determined during the back testing phase after the model has been trained on the training dataset. A precision score is determined by comparing the actual target data against the back tested predictions. The complete of accuracy range typically falls within 49% to 54% which is within requirements for the purposes of this project. Accuracy and success of the project were also considered when examining the returns produced by the model when compared to the actual returns of the market. Often the model performs much better or slightly above the market during the back test which is considered a successful outcome for this project.

![Metric Example 3](https://i.imgur.com/SiKKOK9.png) ![Metric Example 3](https://i.imgur.com/wZHd75h.png)

It was observed with the model that is often skewed towards classifying a data point as the closing price going below the previous day closing price. This is also coupled with an obvious skew towards the model classifying a closing price data point as going down when it often goes up. We believe that due to the more split nature of the data (close numbers of 0s and 1s) that a more accurate model would reflect an even heatmap for the 1, 1 and 0, 0 column. Further analysis of the data and the model hyperparameters would be needed to determine the exact cause of the skew. However, this could possibly be due to the model being overfit with the large nature of the dataset or need for more classifying features.
