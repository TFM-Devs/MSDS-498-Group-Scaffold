# MSDS-498-Group-Scaffold
Source repository for MSDS 498 Financial Services Group Project

The idea for this project and repository was to create a lightweight analytics application that allows a user to connect to and pull basic financial metrics for stocks. The technology components for this application are the AlphaVantage stock market API, AWS S3 cloud storage, AWS Cloud9 IDE, AWS Lambda, and Flask. This repository represents a basic minimum viable product (MVP) of one complete round trip pulling financial data from the API, using AWS lambda to transform it and post it to cloud storage as a .csv. Once written to storage the data can be accessed via a simple flask frontend. This MVP is a proof of concept meant to show an example of the capability, there are many ways to expand the feature functionality which the team will discuss pursuing once the project is completed.
I will quickly step through the process. The ultimate source of the data is a the AlphaVantage API. AlphaVantage is a free API that allows a user to connect to and pull financial data. A user can pull information from AlphaVantage such as historical price quotes, historical strength indices, channel indicators (Bollinger Bands for example) and many more. For this project we decided to focus on the relative strength index (RSI) as the metric to focus on. 
RSI provides a measurement of how strong the stock price action is relative to the market overall and relative to historical stock performance. We decided this was a good metric to start with for two reasons. First, it is a single metric that can inform decision making. With RSI it is easy to see quickly what stocks are leading or lagging the market. So, we wanted something that would provide immediate value to the user. Second, RSI can be valuable in both tabular and visual form. For example, a table of stock RSI is as helpful as a line chart showing RSI changes over time. It’s a matter of taste, and when the decision was made to choose a metric we didn’t exactly know what the frontend would be, so we want to stay flexible.

A sample call to pull AlphaVantage RSI is below. You can see that the API calls are lightweight and include only a few required parameters. This was superior to other options, also it is completely free. 

![Group Pic 1](https://user-images.githubusercontent.com/67444022/119279351-02dc6a00-bbe0-11eb-88ea-db669ea04a54.PNG)

Using AWS lambda the team created a lambda function that ran calls for RSI for a few different stocks. After some transformation the results were loaded into a .csv file that was automatically created in a Amazon S3 storage bucket. Below is a sample of code from this lambda function. 

Once the data is loaded into S3 we use a flask app frontend to expose the data to the end user. At that point, the user can enter a stock ticker symbol and see the result of the RSI indicator shown on the screen. 

More information about AlphaVantage and what other indicators can be pulled using the API can be found at:
https://www.alphavantage.co/documentation/
