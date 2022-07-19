**22-07-14--12:41:22**

Have now done several runs using 10 epochs to evaluate the best learning rate / bitwidth combination. Every time, the best learning rate is the highest one in the range because it produces the largest drop in the loss function over this smaller training period , while smaller learning rates have not had enough time to converge. 

```{figure} images/learning_rate_example.png
---
height: 200px
name: learning_rate_example

---
The best learning rate always appears to be 0.01 when the training only lasts 10 epochs
```

As a result, on the next run, I will change the number of epochs to 50 (but keep the smaller step number) in order to try and find the optimal learning rate for this length of training. Everything else will be kept constant.

**22-07-14--14:41:43**

- learning rates tested: 0.003, 0.001, 0.0003, 0.0001, 0.00003, 0.00001
- bitwidths tested: 12, 16
- Using 50 epochs during search

Had not processed validation set correctly so all previous trials are not useful.

**22-07-14--15:25:45**

- learning rates tested: 0.003, 0.001, 0.0003, 0.0001, 0.00003, 0.00001
- bitwidths tested: 12, 16
- Using 50 epochs during search

Getting some much better loooking training curves, volatility has decreased and the validation loss is decreasing fairly consistenly across all 50 epochs.

```{figure} images/220714_152545_tbsummary.png
---
height: 200px
name: learning_rate_example

---
Optimal learning rate appears to be around 0.003 for both 12 and 16 bitwidth
```

Have fully trained the best model from this search and plotted the graphs to check how it performs. 