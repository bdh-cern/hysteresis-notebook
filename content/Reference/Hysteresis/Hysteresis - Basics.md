
## SFTPRO1 hysteresis loop

Anton liked showing the hysteresis like so, i.e. by looking at the loop swept in one full SFTPRO1 cycle, and subtracting the 'anhysteretic curve' which he took to be the linear-ish median value of the loop:

![[Pasted image 20260917112830.png]]

This loop really demonstrates the dynamic hysteresis only, since it is acquired all from one cycle. 


# Hysteresis on injection

Traditional wisdom claims predicts some static hysteresis on the SFTPRO1 injection plateau. However, the plateau is the period of maximum B-train drift, because the NMR drift correction only applies at the start of the ramp.

![[Pasted image 20260918162940.png]]

This must be caused by a difference in noise when adding in the LHC cycle, which matches experience from [[06-05-26 MD - Magnetic Calibration, Flat-top Studies]]. 

Looking at a wider slice, the injection plateau eddies don't seem to vary much either. Only the pilot cycle (with many ZEROs before the next MD1-SFTPRO1) has a really difference. Will have to check this over other SC changes.

Will have to triple-check that there's no trims going on in here.

![[Pasted image 20260918174057.png]]