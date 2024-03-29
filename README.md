#  Stock Pattern Analysis :money_with_wings::chart: </p>
<img src="https://user-images.githubusercontent.com/112334326/228930065-efd1f97d-f843-46d4-96db-8b0527d3bb4d.png"  width="1200" height="200" />
This repository is dedicated to explain about my project on analysis and create the Machine learning model to clustering the stock pattern and adapt it with trading strategy. Moreover, This is one of the final project of the data master course that we have only about 1 week to finish it!

## Related Tools :toolbox:
- Python 3.10.6
- matplotlib 3.7.1
- tslearn 0.5.3.2
- pandas 1.5.3
- numpy 1.23.5
- yfinance  0.2.12

## Key Concept :bulb:
<p>The key idea of this project came from the curiousity of mine about why the trader champion can make a profit with the technical data(price, volume). 
  <p align="center">
<img src="https://user-images.githubusercontent.com/112334326/228923597-09f7e839-81c2-44b5-9a86-d3dbf0dc6512.png"  width="400" height="400" />

  </p>
 <p align="center"> Pic 1 How to make  money in stocks(William j o'neil)</p>
  If you have ever read the "trade like stock market wizard"(Mark Minervini) or  "How to make money in stocks" (William j o'neil), you would notice that both O'neil and Minervini use the stock moving pattern(VCP, cup with handle etc.) to specify the right time to take action. Morover, these techniques can adapt with almost the stock in the market. So I think that </p>
  
  >  <p align="center">" Why can't I extract the unique pattern from the desire stock to tell us what we should do next?"</p>
  <p align="center">
  <img src="https://user-images.githubusercontent.com/112334326/228928324-19ed0c5a-23b7-4c5a-9eec-67510a369968.png"  width="500" height="200" />
  </p>
 <p align="center"> Pic 2 Volatility Contraction Pattern(VCP) [1]</p>



The key concept of this project is to extract and clustering the pattern of the desire stock. then, predict the near future trend of each pattern group to tell us what action we should do next.

![image](https://user-images.githubusercontent.com/112334326/228920903-5ca2686e-1f89-4a64-b75d-3a70a2b35499.png)
 <p align="center"> Pic 3 Key Concept of this project </p>
 Moreover, When I initially researched though the internet on how to work with project, I found this project that describe really good about time-series clustering. 
  <p align="center"> 
  <img src="https://user-images.githubusercontent.com/112334326/229558407-1ec52274-115e-4923-bb85-5f1b54a3e825.png"  />
  </p>
   <p align="center"> Pic 4 The reference publication  [2]</p>
 Thank and credit for this guy, my project was based and adapted from this project.
 

## Process
In order to achieve the goal, I divide the step in to 4 main part which is
1. Data preparation and Preprocess
2. Training the Model
3. Evaluation the model
4. Clustering the signal 

<p align="center">
  <img src="https://user-images.githubusercontent.com/112334326/229153654-eeebc56b-c1d9-40b7-b1b9-ccba30821c23.png"   />
</p>
 <p align="center"> Pic 5 The process to train the model</p>
 
### 1. Data preparation and Preprocess
As you know, First step of all data work, preparation of the data for our model. From the datamaster Course, I was provided several of the daily stock close price which are 
- AMZN[Amazon]
- DPZ[Domino pizza]
- NFLX[Netflix] 
- BITCOIN 

from 4 APR 2013 to 14 MAY 2019 . So I chose the NFLX stock to use in my model due to the familiarity and because I am one of their customer :stuck_out_tongue_closed_eyes:. In addition, I fulfiled my data-set by downloading the daily volume from yahoo-finance. Here is the close price plot in graph with simple moving average from 4 APR 2013 to 14 MAY 2019.
<p align="center">
  <img src="https://user-images.githubusercontent.com/112334326/229566739-c39fba4e-ff22-4356-9683-748e157a7e9a.png"   />
</p>
 <p align="center"> Pic 6 NFLX close price(Black) with 20D simple moving average(red) from 4 ARP 2013 to 14 MAY 2019.</p>
 
#### 1.1 Window slice and slide

After we download the data and check none is missing. I began to extract the pattern of from the stock by dividing the stock price in to the n part or "Window" to use in our model show as in the pic 7.

<p align="center">
  <img src="https://user-images.githubusercontent.com/112334326/229568008-b67dd63e-4d86-4725-bb03-35773b60beb9.png"   />
</p>
 <p align="center"> Pic 7 NFLX close price dividing to small window.</p>
Nevertheless, This divided windows alone are not enough to represent the pattern. Because the pattern may change related to the time and the position of the window.To be Clarify, let's see the example below

<p align="center">
  <img src="https://user-images.githubusercontent.com/112334326/229572508-b5f95546-fafb-4e39-a25a-6677cb567ade.png"   />
</p>
 <p align="center"> Pic 8 The diffence of the window by vary the start time</p>
 
 Pic 8 show us the two diffent window which have diffent starting point. As you can see, If we change the starting point of the window from 24 APR 2013 (pink frame) to 10 MAY 2013(yellow frame). the pattern of the data that we divided is change. That's why we need to slide the window to cover most of the pattern.

#### 1.2 Mean-Variance Scaling
After we divide the stock signal in to the window. The signal in each window has different level of the price. In this project, we will focus on only the moving pattern and the volume. So we will normalize all the divided price window by using mean-variance scaling.

### 2. Training Model
Training a model is essential part of the project. If we choose the unsuitable model, the result would might not be good like we thought. In this project I use the Dynamic time warping(DTW) algorithm with the TimeseriesKmeans to clustering the price pattern.
#### 2.1 Dynamic Time Warping Algorithm (DTW)
Have you ever wonder how the google assistant or siri can distinguish between when you say "Pencil" and "Peeeennciiiiill"? The Dynamic Time Warping is one of the algorithm behind these AI. The Dynamic Time Warping is an algorithm that measure the similarity between two different timeseries signal. Unlike the Euclidean distance, DTW can map the first and second signal by one-one, one-many or many-one relation as show in Pic 9. And by this property, DTW can adapt with the application like speech-recognition. 
<p align="center">
  <img src="https://github.com/Kritkikomo/StockPatternAnalysis/assets/112334326/5a3e7d04-b43a-46b4-90cd-27d17f74cbe2"  width="250" height="300" />
</p>
 <p align="center"> Pic 9 Euclidean Matchin and Dynamic Time Warping Matching[3]</p>
 So from the application, I thought this algorithm is suitable for our model because sometimes the pattern of the stock price do not have possess the same amout of time. As you can in Pic 10 the price pattern form in the same cup with handle pattern.However, the time and the dept of the cup are not the same in cup A and B. That is why DTW is the key role to overcome these problems.
 
<p align="center">
  <img src="https://github.com/Kritkikomo/StockPatternAnalysis/assets/112334326/263adf05-4698-4b0c-ab01-fa6ee2dff95c"   />
</p>
 <p align="center"> Pic 10 The cup with handle pattern </p>
 
#### 2.2 TimeSeriesKMeans
After we got the DTW algoritrhm. Next, we use the <a href ="https://tslearn.readthedocs.io/en/stable/user_guide/clustering.html#k-means-and-dynamic-time-warping">TimeSeriesKMeans</a> library to cluster the all the window data that we prepared in step 2. The parameter that I focused are window size which is size of the data in one window, the window slide step the step that window was slided for each time, and the number of the cluster.
### 3.Evaluation the model
#### 3.1 Evaluate and optimize the model
It's time to optimize our model! I choose <a href = 'https://tslearn.readthedocs.io/en/stable/user_guide/dtw.html'>the mean of the DTW </a>to be the measurement metric. The Pic 11 show us the DTW score of the result trained model which I tuned with the window slide step, window size and the number of cluster. 
<p align="center">
  <img src="https://github.com/Kritkikomo/StockPatternAnalysis/assets/112334326/da8503c6-a791-49dd-a9d0-b5f04d07bd8f"   />
</p>
 <p align="center"> Pic 11 The DTW of each pair signal in each group</p>  
The Y axis show us the nth number of the pair in that cluster and the X axis show us the return DTW score of that pair. Remind you that the lower DTW score, the more likeliness. At last, I choose the the model which have the window size of 20 , step size of 10 and the 15 cluster to be the tester of the system.
<b>You might wonder why I did not choose the 1 step size and 15 cluster. the cluster look distributes equally and the DTW score is look perfect.</b> 
<p align="center">
  <img src="https://github.com/Kritkikomo/StockPatternAnalysis/assets/112334326/5d413a03-4603-48e9-8f67-1e2f598037f7"   />
</p>
 <p align="center"> Pic 12 The resulted signal after cluster</p>  
 You can see in the Pic 12 that after we cluster. there are a greatly amount of noise in each cluster. This happens because the window was slided to frequent. And it effect the resulted clustering model make the signal in the cluster group not precise.That's why I do not use the model with to frequent window slide.
 
### 4. Clustering the signal 
After I pick the test cluster. I visulize the each signal in the cluster to see the likeliness in the cluster as show in Pic13. 
<p align="center">
  <img src="https://github.com/Kritkikomo/StockPatternAnalysis/assets/112334326/9992efc4-d9d7-40f4-a5be-b47fdd16dad6"   />
</p>
 <p align="center"> Pic 13 The clustered signal with the trend probability</p>  
In the Pic 13, If you can see, I also add the probability of the price trend into each cluster. These probability come from the historical data by using the maximum day that signal stay continuously above or below the simple moving average(SMA) trend line in next period window (In this case next 20 days). For example if the price of the next 20 days stay above sma for 10 days, go random for 5 days (go above and below the SMA)and stay below SMA for 5 day.In this case we will consider the trend to be uptrend.

#### 4.1 Test the model
I choose the same NFLX stock but alter the test data from the train between 14 May 2019 to 14 May 2021. Then, I use the model to clustering the 20 window size of price every 5 day to see what cluster of the signal are and use the probability of the trend that we gather to take action. 
<p align="center">
  <img src="https://github.com/Kritkikomo/StockPatternAnalysis/assets/112334326/6344503a-882a-44fe-8ed2-4cb3116230bf"   />
</p>
<p align="center"> Pic 14 The trading test  with the model</p> 
At the end, the model works just fine. we can overcome the buy and hold strategy for 10% more profitable as you can see in Pic 14. However, the result is very surprising for me because at first I think there is a chance that this Idea might not work as well.

#### 4.2 Further development
I think there is more room for improvement. As you can see, this model is test only one stock at one period of time. There have several parameter that we should focus as well such as risks(drawdown) or the compatibility of the model with other stock. If you read until the end thank for your interest. And if you want to discuss with me you can direct message via my linkedin below. Cheer:tada::tada:!!!

Mylinkedin : <a href='https://www.linkedin.com/in/chakrit-wanth/'>chakrit-wanth</a>



Source
[1] https://www.vantagemarkets.com/en-au/education/how-to-trade-volatility-compression-patterns-vcp/

[2] https://pub.towardsai.net/time-series-clustering-for-stock-market-prediction-in-python-part-1-738ab6462f0e

[3] https://commons.wikimedia.org/wiki/File:Euclidean_vs_DTW.jpg
