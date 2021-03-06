## Background

We first tried to recreate "Predicting digital asset market based on blockchain activity data" found [here](https://arxiv.org/pdf/1810.06696.pdf).

After multiple roadblocks, we were able to start the initial sync with Parity Client. After 24 hours at full CPU usage, the initial sync was not even half complete. 

As a result, we decided to recreate a similar project, "Predicting Cryptocurrency Prices With Deep Learning" found [here](https://dashee87.github.io/deep%20learning/python/predicting-cryptocurrency-prices-with-deep-learning/).

Although this second source is not technically a "research paper," it is a good example of real world experience with deep learning. It is also extremely readable and requires very little technical roadblocks to setup.



## Summary of Original Paper
The original blog uses a Long Short Term Memory (LSTM) model to predict the price of Bitcoin and Ethereum using data pulled from coinmarketcap.com. The model was trained on data from before June 1st 2017 and tested on the data after (Up to November 2017). The training data set was very limited in that the price of the cryptocurrencies generally only steadily increased. Also the training set lacked data that any big spikes present like the rapid rise of the Cryptocurrency market in late 2017 and the subsequent crash in 2018.

The training of the model was done by feeding it windows of data containing 10 days worth of data at a time. The data is normalized between -1 and 1 before being used as inputs. Using 20 neurons in the LSTM layer and 50 epochs, the model achieved a mean absolute error (MAE) of 0.0531 on the test set for Ethereum, and 0.0392 on the test set for Bitcoin in single point predictions. The model also tends to overestimate the value in general and has difficulties predicting spikes and troughs. There was also a test set for 5 timepoint predictions that showed less appealing results but showed some 'nuanced' behaviour in that it didn't simply predict prices to move in one direction.

The blog also discusses simpler models such as a lag model and random walk model to compare to the LSTM model and warn against how easy it could be to generate a visually appealing model with no substance behind it to back it up. The author ends the blog by offering some skepticism about using deep learning to predict cryptocurrency prices and suggesting some possible changes to improve the model.


## Steps to Reproduce Original Experiment

Since the blog post provided a Jupyter Notebook with code and explanation on how to reproduce the experiment, it didn't take too many steps to get everything working. Here are the steps we took (using a Windows machine):

1. Download Repo located [here](https://github.com/dashee87/blogScripts)
2. Open Jupyter Notebook titled: 2017-11-20-predicting-cryptocurrency-prices-with-deep-learning located in the Jupyter folder.
3. Using Anaconda Prompt:<br/>
  a. Install Keras and Tensorflow<br/>
  b. Update Conda<br/>
  c. Downgrade Pandas to version 0.23.4<br/>
4. Install any other libraries using pip that throw an error in the Jupyter Notebook
5. Uncomment block 37 in Jupyter Notebook
6. Restart and run Jupyter Notebook
7. Wait until everything finishes (could take a few hours)

## Results of Original Experiment
<p align="left">
  <img src="https://i.ibb.co/TtfxxwZ/Training-Testing-Set.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/Wy2F6wb/Simple-Lag-Model.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/wB9jygY/Single-Point-Random-Walk-Test-Set.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/RPvHyVk/Full-Interval-Random-Walk.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/4SBLtcb/Single-Point-Random-Walk.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/j3brqPx/Training-Error.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/82K3n32/Training-Set-Single-Point-Timepoint-Prediction.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/TwqDLQR/Test-Set-Single-Timepoint-Prediction.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/KNzj3KD/Training-Set-Single-Point-Timepoint-Prediction-Bitcoin.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/3rxGZXP/Test-Set-Single-Timepoint-Prediction-Bitcoin.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/FVTR385/Test-Set5-Timepoint-Predictions.png">
</p>
<p align="left">
  <img src="https://imgbb.com/"><img src="https://i.ibb.co/dcVy8VL/MAECharts.png">
</p>

## Differences From Original
1. Since we ran this experiment almost two years after the original, there was a lot more test data.
2. Full Interval Random Walk for Ethereum didn't produce correct "actual" data.
3. Training and Testing Single Timepoint Prediction MAE's for Ethereum were lower (more accurate). Especially on the test set.
4. Training and Testing Single Timepoint Prediction MAE's for Bitcoin were lower (more accurate).
5. The 5 Timepoint Predictions seemed more accurate, especially for Ethereum.
6. Bitcoin and Ethereum 25 Test Set Runs had lower MAE's (more accurate).
7. Axis titles and formatting were different from original experiment.

## Reflecting on Differences
Since there is more testing data (which includes the crash), there is more for the models to validate against. This can cause a better accuracy on testing due to the new fluctuation in the test data. Having more testing data also gives formatting problems due to so many titles on the x-axis.

## Changing Aspect of Original Experiment
Since this experiment was trained on data that happened before the cryptocurrency rise and fall of late 2017 and early 2018, we decided that it would be beneficial to split the data after the crash. We chose 08-01-2018 to split the data on. We chose this specific data since there was a lot of fluctuation after the crash and it started to stabilize more around this time. Also, this experiment made it easy to change the split date.

## Results of Modified Experiment
Instead of including every chart like above, we chose the most relevant charts to show differences from the original experiment.

<p align="left">
  <img src="https://imgbb.com/"><img src="https://i.ibb.co/ngnSPwQ/Training-Testing-Set-Final.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/Wg6dg99/Training-Error-Final.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/9sGr5jn/Test-Set-Single-Timepoint-Prediction-Final.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/fdZ2sKf/Test-Set-Single-Timepoint-Prediction-Bitcoin-Final.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/pdFYSRr/Test-Set5-Timepoint-Predictions-Final.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/16QPBr2/MAECharts-Final.png">
</p>

## Explanation of Modified Experiment Result
Since we now have more data to train on, our chances of overfitting the data decreases. The added diversity of the new train data helps better the fit and as a result, the accuracy improves. As you can see from the charts, the training accuracy has improved, and the test set accuracies for both Ethereum and Bitcoin have also improved. The MAE over the 25 runs for Bitcoin has been improved to less than 0.025 and Ethereum has improved to less than 0.040. Since cryptocurrency prices have steadied after the split date, it is surprisingly accurate since it has been trained on volatility.

## Other Modifications and Results
Since Ethereum and Bitcoin are both relatively stable cryptocurrencies, we thought it would be a good idea to train and test on a highly volatile cryptocurrency. We chose Tron since it is pretty well known as the top volatile coin. We wanted to see how much different the accuracy of the model runs would be versus the more stable coins. Below are the important charts:

<p align="left">
  <img src="https://i.ibb.co/rbjXBbm/trontrainingerror.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/L1xSn8d/tronsinglewalktestset.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/Hrb85vh/tronsingletimepointtestset.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/R26jz1q/tron5testset2.png">
</p>
<p align="left">
  <img src="https://i.ibb.co/cbK0q1q/tron25runs.png">
</p>

## Explanation of Other Modifications and Results
As you can see, the model had a much tougher time training and testing on Tron. The Single Point Random Walk Test Set was very sporadic and different from the other cryptocurrencies tested. The 5 Timepoint Predictions also show many more inaccurate predictions. The overall MAE over 25 runs was also almost twice of that of Bitcoin. Our prediction that LSTM would have a harder time on Tron was validated through this experiment.

## References
1. https://arxiv.org/pdf/1810.06696.pdf
2. https://www.researchgate.net/publication/329322600_Prediction_of_Cryptocurrency_Returns_using_Machine_Learning
3. http://lup.lub.lu.se/luur/download?func=downloadFile&recordOId=8962155&fileOId=8962156
4. https://medium.com/datadriveninvestor/predicting-cryptocurrency-prices-with-machine-learning-1b5a711d3937
5. http://www.eumetrain.org/data/4/451/english/msg/ver_cont_var/uos3/uos3_ko1.htm
6. https://activewizards.com/blog/bitcoin-price-forecasting-with-deep-learning-algorithms/



