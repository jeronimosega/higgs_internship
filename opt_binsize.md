# Investigating the effect of image resolution on model performance
*CMS data was used for training and testing the models*

## Method
The image dataset consisted of 200,000 images with a resolution of $120 \times 72$ pixels. From this dataset 4 pairs of training and testing data were created with resolutions varying from $20 \times 12$ pixels up to the full $120 \times 72$ pixels:

- $20 \times 12$
- $40 \times 24$
- $60 \times 36$
- $120 \times 72$

Using the Keras and QKeras libraries, a CNN model was trained on each resolution in order to assess how the performance of the model would be affected. The architecture and hyperparameters of the model were kept the same for each trial.

## Analysis

### Signal Efficiency
The **signal efficiency** is equal to the true positive rate of the models predictions. It is measured at various **trigger rates** and then plotted as shown in figure 1.

```{figure} images/Kmodel_efficiencies.png
---
height: 200px
name: Kmodel_efficiencies

---
Signal efficiency vs Trigger rate graphs for Keras models
```
```{figure} images/Qmodel_efficiencies.png
---
height: 200px
name: Qmodel_efficiencies

---
Signal efficiency vs Trigger rate graphs for QKeras models
```

### Background Rejection
These graphs show the rate at which background events sare predicted as signal for varying thresholds of certainty. 

```{figure} images/Kmodel_rates.png
---
height: 150px
name: Kmodel_rates
---
Trigger rate vs Threshold AU for Keras models
```
```{figure} images/Qmodel_rates.png
---
height: 150px
name: Qmodel_rates
---
Trigger rate vs Threshold AU for QKeras models
```

## Results

### How resolution affects performance

With the exception of the $60 \times 36$ QKeras model, it is clear that increasing the resolution of the images that are fed to the model will improve its performance in both signal efficiency and background rate rejection. 

### Difference between Keras and QKeras models

Interestingly, the Keras models performed better across all resolutions in terms of signal efficiency (at the target efficiency of 10kHz). However, the QKeras models generally performed better at background rejection

## Conclusions

From the graphs it is easy to conclude that the models which were shown images with higher resolution saw increased performance across the board. Therefore, if it is possible to complete a firmware build for these larger histograms, using an increased resolution would be an easy way to improve the performance of this model architecture without having to change any of the hyperparameters.

















