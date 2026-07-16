See also:
[[06-05-26 MD - Magnetic Calibration, Flat-top Studies]]
[[23-06-2026 MD - Testing Drift Corrector]]
[[LHC -> SFT Drift]]
[[Dodgy Drifts]]
[[29-05-26 - Temperature Considerations]]
[[17-06-26 - Drift Fitting]]

# Overview

Created a UCAP device which corrects for the drift on SFTPRO.

Subscriptions:

```
SR.BMEAS-SP-B-SD/SamplesFromTrigger
BCTECO/Acquisition
SX.CZERO-CTML/SuperCycle
rmi://virtual_sps/SPSBEAM/B
rmi://virtual_sps/SPSBEAM/BHYS
```

Trims BHYS using an actor:
```
"actors": [
        {
            "name": "PublishBHYSCorrectionToLSA",
            "description": "Publishes to the correction of BHYS on LSA",
            "transformationProperty": "BHYS",
            "action": {
                "language": "Java",
                "className": "cern.ucap.actions.standard.lsa.LsaTrimAction",
                "configuration": {
                    "useElevatedRbacContext": false
                }
            }
        }
    ],
```

BHYS is in the LSA hierarchy such that it and SPSBEAM/B are summed before being converted to IMAINS:

![[Pasted image 20260709164805.png]]

The incorporation rules for BHYS are such that it is linearly ramped from the start of the flat-top to the incorporation point and constant thereafter. This approach was chosen because of concerns over disturbing the ramp (specifically transition). Since the converters can't ramp too quickly, I am using an incorporation point at 5000ms, about half a second after the start of the flat-top. It's possible that this could cause issues. In [[06-05-26 MD - Magnetic Calibration, Flat-top Studies]], we just raised SPSBEAM/B by a flat amount and had no issues with the ramp (despite it presumably being altered by this sort of trim) so maybe we can relax this constraint if needed.

# Naive Approach

First used a very simple method which just calculated the delta and applied that to the next cycle:

$$
\begin{align*}
\Delta &= \textrm{BMEAS} - \textrm{BTARGET} \\
&= \textrm{BREF} + hys + \textrm{BHYS} + sys - (\textrm{BREF} + sys) \\
\Delta &= hys + \textrm{BHYS} \\
\textrm{BHYS} - \Delta &= -hys \\
\end{align*}
$$
	Where:
		- BMEAS is the measured field from the BTRAIN
		- BTARGET is the desired B
		- BREF is the programmed B (SPSBEAM/B)
		- BHYS is SPSBEAM/BHYS
		- *hys* is the field causes by hysteretic effects
		- *sys* is the systematic error between the B-train and the programmed B

Tested this in [[23-06-2026 MD - Testing Drift Corrector]] with good results.

![[Pasted image 20260709165358.png]]

# Model-Based Prediction

Used the fits from [[17-06-26 - Drift Fitting]] to make a model-based version which predicts the field using a triple exponential fit.

$$
y(t) = A_1e^{-k_1x} + A_2e^{-k_2x} + A_3e^{-k_3x}
$$
Where the time constants $\tau =1/k$ come out to about 1.5, 20, 150 cycles. I interpret this as static hysteretic accommodation, slow drift of the static hysteresis (fast) caused by the cumulative dynamic effects (slow), and possibly a temperature term (medium). Of course, there's no reason that the real effects would have to break down nicely into these three exponential terms.

This works by continuously comparing the correction that the model would give and that which the naive approach would give and choosing its strategy accordingly. This approach saves a few cycles at the start of the supercycle. When testing with historical data, it typically returns to the naive method after 7 cycles or so.

![[Pasted image 20260709163614.png]]

Comparison of the type schemes:

![[Pasted image 20260709164026.png]]

It would be good to establish models for other SCs. It's probably possible to predict each decay based on a triple exponential and the initial field (which would mean we don't need to know what the previous supercycle was).
# Timing Improvements

Because the device is currently subscribed to the B-train as trigger, it only first after the first cycle has already finished. Will need to change this to one of the pre-warned timing signals so that the first cycle can also be fully flattened.

I'm currently getting the SC users from SX.CZERO-CTML. There are timing devices which pre-warn the next cycle up to 2000 ms, but none that pre-warn the supercycle. Therefore this feature will probably have to wait.

# Dealing with Spare Cycles

It's fairly simple to add an exception for spares. I just need to check the actual user against the same position in the expected supercycle, and if there's any difference, I reset BHYS to 0.0. This is a low-priority feature so I won't implement it yet.

# Testing with Full Sequences 

This clearly demonstrates the need for the one-SC look-ahead.

![[Pasted image 20260713130620.png]]

Can check what the particle is listed as in NXCALs during the no beam events for additional info.

![[Pasted image 20260714182003.png]]


- Made some adjustments to catch those spikes. Namely, if the next SC is also correctable then BHYS will not be zeroed. This is nice because the first SFTPRO of the SFT SC still needs the same BHYS as would have been applied to last SFT in the LHC SC. The one-cycle time lag applies this in the correct position.
- Wondering why the correction is not zeroed on the unclassified SCs now. Also why are there any points in there at all since I thought it was just LHCION, MD1, and ZERO? To check.
- Also not quite sure why the BHYS eases off after the nans around 0230AM nor why the model-based correction turns on here.
- Clearly need to improve the model as it only is correcting 1 or 2 cycles now. Nonetheless, it's quite effective.    