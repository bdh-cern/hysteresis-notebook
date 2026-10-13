- Using claude to rapidly prototype a few different types of predictor

# Segmented_Predictor

## Training Data

Getting segments of 10+1 SFTPRO1s (input+output).

Thinking that this is too few for what I'm asking of the NN. The drift constants are longer ([[Slow Hysteresis Drift]]). Therefore, I can't expect this NN to make accurate predictions outside the 10-cycle window around an interface.
	- But surely it could learn that a slow drift of 10 cycles continues slowly, and a fast drift of 10 cycles continues quickly?

Idea: include two new input variables:
	1. Field of last higher-field cycle (e.g. LHC1)
	2. How many cycles ago this occurred.

Issues: how should this handle anomalies such as dyneco, fulleco, etc?

For now, might be best to just train on many many cycles (say, 99+1).

## Dips

![[Pasted image 20260908105759.png]]

Having issues with low dips on SFTPRO1. Claude analysis shows that the dipoles were doing some odd slow ramp during this period (pinch of salt). Regardless, I only trained this data on one day, 15th July, during which I was testing the compensator anyway, so maybe a bad choice.

## Stats

The stats for this technique are not fantastic:
```
target spread on the test set: 0.44 (1e-4 T)
neural_network               RMSE     0.48   MAE     0.19   (1e-4 T)
previous_target_user_field   RMSE     0.48   MAE     0.10   (1e-4 T)
persistence_forecast         RMSE 17004.25   MAE 17004.25   (1e-4 T)
training_mean                RMSE     0.53   MAE     0.36   (1e-4 T)
  steady     examples:   728   RMSE     0.48
```

## Large Dataset

Using several months of data, the results are not much better.

```
target spread on the test set: 3730.96 (1e-4 T)
neural_network               RMSE   388.80   MAE    38.96   (1e-4 T)
previous_target_user_field   RMSE   545.34   MAE    17.08   (1e-4 T)   (206 skipped)
persistence_forecast         RMSE 16560.32   MAE 16151.54   (1e-4 T)
training_mean                RMSE  3732.52   MAE  1697.35   (1e-4 T)
```

![[Pasted image 20260908134513.png]]


Dips in the predicted accuracy, but no change in the measured, showed that the NN was learning based on input node indices, i.e. it was encoding the fact that the last cycle before the SFTPRO1 was an MD1, the one before that was high-energy, then MD1, etc.

If the SC changed away from this arrangement, it would cause prediction issues until the arrangement was restored. 

![[Pasted image 20260908134856.png]]

# Transfer Function Predictor

The transfer function predictor appeared to work well:

![[Pasted image 20260909104833.png]]

However, on closer inspection, most of its goodness is coming from the easy steady-state sections:

| target current NOT represented | RMSE     | MAE      |
| ------------------------------ | -------- | -------- |
| neural_network                 | 0.031710 | 0.008497 |
| operating_point_lookup         | 0.025334 | 0.006209 |
which shows that when the NN has to predict the transfer function for a current outside the input window (e.g. near an interface), it fails compared to just looking up a table of (cycle_name, current) => transfer fuction.

Also we have:

| target current represented in window | RMSE     | MAE      |
| ------------------------------------ | -------- | -------- |
| neural_network                       | 0.002836 | 0.000847 |
| same_operating_point_copy            | 0.002222 | 0.000403 |
which means that in slow drift sections, it's more efficient to just look up what the last SFTPRO was at instead of trying to predict it from the NN.

The stats for 'target current NOT represented' are a little suspicious to me because this is precisely the scenario in which a look-up should fail.

Further analysis shows that (most of) these unrepresented states occur when the SC is longer than the 10 cycles of input the NN gets. Retraining with an input length of 30 cycles stops the 'unrepresented' flag from firing here, and it now more accurately represents instances where the current hasn't been in history (i.e. near an SC change):

| target current represented in window | RMSE     | MAE      |
| ------------------------------------ | -------- | -------- |
| neural_network                       | 0.093949 | 0.033518 |
| same_operating_point_copy            | 0.074233 | 0.037129 |

Now the MAE is slightly better, but the RMS is still worse. As the RMSE is more sensitive to outliers, this implies that the NN is actually doing its job generally, but it fails on some specific instances. Claude analysis has found that every such outlier consists of 30 zeroes (both zero-cycles and cycles which didn't play due do e.g. fulleco) followed by an MD1. This makes sense: I have only included field maxima in the training set, with the return to zero-current being null-info because it happens after every single cycle. However, this breaks down if the zero-cycle is included in the training set, because now this null-info is partially being included. In other words, I can either fully include or fully exclude this useless information; if I include it half of the time, the NN will learn on it. 

Filtering zero-cycles results in a much better predictor:

| target current represented in window | RMSE     | MAE      |
| ------------------------------------ | -------- | -------- |
| neural_network                       | 0.029733 | 0.028309 |
| same_operating_point_copy            | 0.069213 | 0.061984 |

However this MAE still gives +-140G for these examples.

Bear in mind that SFTPRO1 near an interface is not 'unrepresented', as it will generally occur before the interface as well. If we look at SFTPRO1 within 50 cycles of an interface change, the picture is not flattering:

```
85500 SFTPRO1 test examples, of which 2458 are within 50 cycles of a supercycle change (1.333% of the whole test set)

SFTPRO1, within 50 cycles of a change (2458, spread 0.000426 = 2.06 G)
  neural_network                 RMSE 0.002073  MAE 0.000678   |  RMSE   10.00 G  MAE    3.27 G
  same_operating_point_copy      RMSE 0.000550  MAE 0.000236   |  RMSE    2.65 G  MAE    1.14 G
  operating_point_lookup         RMSE 0.000951  MAE 0.000638   |  RMSE    4.59 G  MAE    3.08 G
  previous_transfer_function     RMSE 0.095131  MAE 0.094832   |  RMSE  458.80 G  MAE  457.36 G
  training_mean                  RMSE 0.041180  MAE 0.041178   |  RMSE  198.60 G  MAE  198.59 G

SFTPRO1, more than 50 cycles after a change (83042, spread 0.000207 = 0.97 G)
  neural_network                 RMSE 0.000412  MAE 0.000187   |  RMSE    1.99 G  MAE    0.90 G
  same_operating_point_copy      RMSE 0.000416  MAE 0.000128   |  RMSE    2.01 G  MAE    0.62 G
  operating_point_lookup         RMSE 0.001150  MAE 0.000784   |  RMSE    5.55 G  MAE    3.78 G
  previous_transfer_function     RMSE 0.095059  MAE 0.094997   |  RMSE  458.45 G  MAE  458.15 G
  training_mean                  RMSE 0.041359  MAE 0.041359   |  RMSE  199.47 G  MAE  199.47 G
```

Analysis shows that this is due to the network training positionally (see above somewhere) and the positionality then being broken when the SC changes (e.g. two SFTPRO1) in a row. I originally tried to remove this by training on every cycle, but this didn't actually remove it, it just made it conditional on the input current of the predicted cycle, since that current encoded the cycle type, and for a set output cycle type the input positions matched certain cycles, as before. Thus if I was predicting SFTPRO1, the inputs were fully positional again.

# Data Issues

See [[NMR Issues]] for now.

# Curve Predictor

Explored the idea of fitting some curve to the B/I plot, and then predicting its parameters. Two issues:

1. My initial instinct of an exponential saturation curve doesn't work very well, and I don't know what to use instead - solvable.
2. The B/I curve for any given cycle is dominated by dynamic hysteresis, which is probably not what we want to predict.
3. The change in parameters over the curve will be very slight.



