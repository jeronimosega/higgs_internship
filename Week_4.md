# Volatility vs Bitwidth


# Creating tuning Jupyter Notebook


# Start to look at learning rate


# Research



# Next week

- Look at the effect of batch normalisation on quantised models. May be degrading performance
- Train 8 and 16 integer bit models as recommended in the study to see how they perform with our architecture
- Train a good Keras Model which can be post-training quantised to provide a starting point for the weights of the QKeras models
- Look at using batchnorm with inference to reduce volatility
- Can obtain improved accuracy by not constraining the ranges of the activations during training and then quantizing them. Use higher precsion for activiations to improve overall accuracy
- Quantise layers, one by one, to try and see which layers are most sensitive to quantization

