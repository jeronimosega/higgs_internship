# Investigating the effect of bitwidth on model performance and validation loss volatility during training
*Delphes simulation data was used to test and train all models*

## Introduction
From the previous investigation into the effect of image resolution on model performance, it was evident the Keras models generally performed better than the quantised QKeras models. This investigation will look at the effect that using different bitwidths has on the model performance, and the volatility of the validation loss during training. QKeras also gives the option to specify the number of those bits that are to the left of the decimal point (integer bits), so This will also be varied to see what  effect, if any, it will have on the model.

## Method
A total of 35 quantized keras models were trained with bitwidths varying from 4 to 16, and with either 1, 2 or 4 integer bits. The same graphs as before were then plotted for each model to try and quantify the performance. The table below outlines which combinations were tested.

|Bitwidth | Integer bits |
|:--------| ------------:|
|4|1, 2|
|5|1, 2|
|6|1, 2, 4|
|7|1, 2, 4|
|8|1, 2, 4|
|9|1, 2|
|10|1, 2, 4|
|11|1, 2|
|12|1, 2, 4|
|13|1, 2, 4|
|14|1, 2, 4|
|15|1, 2, 4|
|16|1, 2, 4|

The volatility during training the models was also kept in consideration because even if the model is good, it need to be able to be reproduced. With very high volatilities, it is very difficult to gauge whether two identical models will acutally perform in a similar manner once they have been trained.

## Results




