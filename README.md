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
After we divide the stock signal in to window. The signal in each window has different level of the price



Source
[1] https://www.vantagemarkets.com/en-au/education/how-to-trade-volatility-compression-patterns-vcp/

[2] https://pub.towardsai.net/time-series-clustering-for-stock-market-prediction-in-python-part-1-738ab6462f0e
