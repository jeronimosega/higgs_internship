# Title

## Subtitle

### 2022-07-18--15-05-00

- 16,6 bitwidth for all layers apart from dense with 8,4
- batchnorm off

**Results**
- produced very smooth loss, must be due to the removal of batchnorm
- need to check by using batchnorm will same other params

### 2022-07-18--15-21-27
- Same as previous except bathnorm on. 

**Results**
- Much more volatile loss curve as we were seeing before
- Will now try to decrease the bitwidth to see how low we can go while still acheiving good performance and a smooth loss curve

### 2022-07-18--15-50-44
- conv_bw = '(8,4)'
- dense_bw = '(8,4)'
- act_bw = '(16,6)'
- bn_bw = '(16,6)'
- batchnorm False

Training curve was slightly odd, mostly followed training loss but massive fluctuation at the  end. Not great performance.

### 2022-07-18--16-28-51
- conv_bw = '(16,4)'
- dense_bw = '(8,4)'
- act_bw = '(16,6)'
- bn_bw = '(16,6)'
- batchnorm True
- Removed batchnorm from the output layer to see if this could have been affecting the prediction of the final neuron

- Training curve appears much better, still more volatile than with no batchnorm but it looks much more normal / closer to Keras Models

### 2022-07-18--16-36-12
- conv_bw = '(16,4)'
- dense_bw = '(8,4)'
- act_bw = '(16,6)'
- bn_bw = '(16,6)'
- batchnorm False
- dropout = 0.2
- lr = 0.001

**Results**
- Very smooth training curves
- Lowest loss of all so far
- Graphs look pretty good, nothing special

### 2022-07-18--16-42-28
- conv_bw = '(16,4)'
- dense_bw = '(8,4)'
- act_bw = '(16,6)'
- bn_bw = '(16,6)'
- batchnorm False
- dropout = 0.2
- lr = 0.002

**Results**
Nice curve, very similar performance overall to previous one. Would consider using variable learning rate to improve this any further.

### 2022-07-18--16-57-19
- conv_bw = '(8,4)'
- dense_bw = '(8,4)'
- act_bw = '(16,6)'
- bn_bw = '(8,4)'
- batchnorm True
- dropout = False
- lr = 0.001

**Results**
-  Terrible, bitwidth was too low

### 2022-07-18--17-01-19
- conv_bw = '(12,2)'
- dense_bw = '(12,2)'
- act_bw = '(16,6)'
- bn_bw = '(12,2)'
- batchnorm True
- dropout = False
- lr = 0.001

**Results**
- Very nice curve and low final loss ~0.05
- Signal effieciency not great compared to others

### 2022-07-18--17-07-54
- conv_bw = '(12,2)'
- dense_bw = '(12,2)'
- act_bw = '(12,2)'
- bn_bw = '(12,2)'
- batchnorm True
- dropout = False
- lr = 0.001

**Results**
- Nice curve, lowest loss so far 
- Great signal efficiency (>0.9), decent background rejections
- Best model so far probably

### 2022-07-18--17-07-54
- conv_bw = '(12,2)'
- dense_bw = '(12,2)'
- act_bw = '(12,2)'
- bn_bw = '(12,2)'
- batchnorm True
- dropout = False
- lr = 0.001
- f1 = 8
- f2 = 16

**Results**
- Good background rejection but slightly worse on sginal efficiency

## Now want to check whether using dropout instead of batchnorm can produce more stable results at lower bitwidths and also if it will degrade performance.

### 2022-07-19--09-55-36
- conv_bw = '(8,2)'
- dense_bw = '(8,2)'
- act_bw = '(16,6)'
- bn_bw = '(8,2)'
- batchnorm False
- dropout = True
- lr = 0.001
- f1 = 8
- f2 = 16

**Results**
- Still smooth
- Good background rejection and good signal efficiency at 10kHz of about 0.9.
- Will try to push even lower

### 2022-07-19--10-03-12
- conv_bw = '(6,1)'
- dense_bw = '(6,1)'
- act_bw = '(12,4)'
- bn_bw = '(6,1)'
- batchnorm False
- dropout = True
- lr = 0.001
- f1 = 8
- f2 = 16

**Results**
- Not the best training curve, accuracy did not end very well and it was fairly volatile. 
- Background rejection was good but signal efficiency low

## Baseline Keras Model
```{list-table} Best Hyperparameters
:header-rows: 1
:name: hypparams-results1

* - Model
  - 20220719--122615
* - Dense layer units
  - 64
* - Activation
  - ReLU
* - L1 Filters
  - 4
* - L2 Filters
  - 8
* - L1 Kernel size
  - 3
* - L2 Kernel size
  - 3
* - Accuracy
  - 0.9898
* - Eff at 10kHz
  - 0.90168



```

## Searching over many bitwidths
In this search I used the Keras Hyberband tuner in order to search over a range of hyperparameters and try to find the best few configurations for this model. The search space was as follows:

```{list-table} Hyperparameter search space
:header-rows: 1
:name: hypparams-search1

* - Hyperparameter
  - Possible Values
* - Bitwidth (conv, dense, bn)
  - (8,4), (10,4), (12,4), (14,4), (16,4)
* - Bitwidth (activation)
  - (12,4), (16,6), (24,8)
* - Learning rate
  - 0.001
* - Activation
  - ReLU
* - Dense layer units
  - 64
* - Batchnorm
  - On
* - Dropout
  - 0
* - L1 Filters
  - 2, 4, 8
* - L2 Filters
  - 4, 8, 16
* - L1 Kernel size
  - 3
* - L2 Kernel size
  - 3

```

The best 5 models from this search had the following hyperparameters:
```{list-table} Best Hyperparameters
:header-rows: 1
:name: hypparams-results1

* - Model
  - Bitwidth (bw)
  - Activation bw
  - L1 Filters
  - L2 Filters
  - Accuracy
  - Eff at 10kHz
* - 20220719--122615
  - (16,4)
  - (24,8)
  - 8
  - 16
  - 0.98696
  - 0.87088
* - 20220719--123510
  - (14,4)
  - (16,6)
  - 8
  - 16
  - 0.98846
  - 0.8632
* - 20220719--124321
  - (16,4)
  - (24,8)
  - 8
  - 16
  - 0.98872
  - 0.8794
* - 20220719--125044
  - (14,4)
  - (12,4)
  - 8
  - 16
  - 0.98646
  - 0.84008
* - 20220719--125511
  - (10,4)
  - (12,4)
  - 8
  - 4
  - 0.98724
  - 0.89512

```



## Problems with current hyperparrameter search
Due to the use of bachnorm, there is still some volatility in the training curve which makes it difficult for the hyperband parameter optimization to correctly pick out the best performing model configurations. As a result, the final models are being produced are overfitting when trained on the full datset and are generally worse than the ones that we usually pick. This may also be due to the fact that in order to speed up the search, the number of steps per epoch is decreased, leading to models which fit to the data faster being prioritized. 

However, by using dropout instead of batchnorm, which previously produced much less volatile training curves which would always steadily decrease, the search will be more likely to find the best performers. This increased stability of the models is also useful for future comparisons.


## Using dropout instead of batchnorm

Seemed fairly obvious from the previous run that all of the best models had higher numbers of filters, especially in layer 1. So for this run, in order to speed up the search process, the smallest number of filters for each layer was removed from the search space. one other advantage of not using batchnorm is that the model is faster and uses less memory due to the removal of the normalisation step. This is important because when it is used, all of the batch statistics must be stored in the layer.

```{list-table} Hyperparameter search space
:header-rows: 1
:name: hypparams-search2

* - Hyperparameter
  - Possible Values
* - Bitwidth (conv, dense, bn)
  - (8,4), (10,4), (12,4), (14,4), (16,4)
* - Bitwidth (activation)
  - (12,4), (16,6), (24,8)
* - Learning rate
  - 0.001
* - Activation
  - ReLU
* - Dense layer units
  - 64
* - Batchnorm
  - Off
* - Dropout
  - 0.2, 0.5
* - L1 Filters
  - 4, 8
* - L2 Filters
  - 8, 16
* - L1 Kernel size
  - 3
* - L2 Kernel size
  - 3

```

The best 5 models from this search had the following hyperparameters:
```{list-table} Best Hyperparameters
:header-rows: 1
:name: hypparams-results1

* - Model
  - Bitwidth (bw)
  - Activation bw
  - L1 Filters
  - L2 Filters
  - Accuracy
  - Eff at 10kHz
* - 20220719--143607
  - (14,4)
  - (16,6)
  - 8
  - 16
  - 0.98482
  - 0.86996

* - 20220719--144343
  - (14,4)
  - (16,6)
  - 8
  - 8
  - 0.98382
  - 0.86212

* - 20220719--145030
  - (14,4)
  - (12,4)
  - 8
  - 8
  - 0.98438
  - 0.8686

* - 20220719--151114
  - (14,4)
  - (12,4)
  - 8
  - 16
  - 0.98534
  - 0.87516

* - 20220719--125511
  - (16,4)
  - (16,6)
  - 8
  - 16
  - 0.98022
  - 0.89024


```