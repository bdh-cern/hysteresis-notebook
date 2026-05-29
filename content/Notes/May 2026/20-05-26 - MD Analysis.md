
- Plot the decays over the last year
- Plot the absolute deltas over the last year
- Take an anomalous decay and work out what's going on there
- Take a normal decay and demonstrate the decay
- Plot the data from the BPMs
# Decays over the last year


- Tried with a window of 1,50 SCs (before/after interface) 
- Normalised to the starting field to fit only the decay
- Worked out the median+-MAD cycles per fit and filtered out fits which used n\<median-MAD cycles
- Ignored cycles affected by dynamic economy using ecoTriggered flag
	- Seemingly this also accounts for full eco as there are no cycles with dumpTime\==0 and ecoTriggered\==0
- Tau = 9.49+-1.81

![[Pasted image 20260520123619.png]]

- Trying also with a window of 1,30 SCs (~90 cycles)
- Tau = 6.958205315916318+-1.0314769816683276
-  This is probably more representative as it is still using a a long time-span (cycle-span) but not too long as to capture as many trims
![[Pasted image 20260520170955.png]]

# Comparing anomalous/nice SC Interfaces

- Looking at the 1,30 data, the interface at 2026-04-14 20:32:06.135 has tau=12
- No obvious anomalies, will have to check logs to see if there were trims etc
- If I squint I can convince myself that this is less of an exponential... there's a steep drop at the start, but afterwards it almost decreases linearly

![[Pasted image 20260520153947.png]]


- Nice interface at 2026-03-22 01:13:04.935 has tau 6.96+-0.43
- No obvious differences to the bad one immediately visible
![[Pasted image 20260520154407.png]]

- Fit:
```
A 3.031979
 0.112815
k 0.143614 
k_err 0.008948
tau 6.963123
tau_err 0.43383
C 17551.197571
C_err 0.02146
r2 0.924194
n 91
readable_time 2026-03-22 01:13:44.535000
cyclestamp 1774138424535000000 dtype: object
```

- Looking at the plot, the fit seems to be a bit too slow at the start and then a bit too fast at the end... this makes a case for using a double exponential instead.

![[Pasted image 20260520175210.png]]


Bad one gives:

```
A 2.860099 
A_err 0.115081
k 0.082745
k_err 0.006103
tau 12.085329
tau_err 0.891366
C 17553.579305
C_err 0.032998
r2 0.90518
n 91
readable_time 2026-04-14 20:32:45.735000
cyclestamp 1776191565735000000
dtype: object
```

- Actually this sort of looks like the first one -- too slow then too fast. Only here there was probably a trim around 40 cycles (or maybe a bad one at 20 cycles) that threw off the decay

![[Pasted image 20260520175713.png]]

There's an even weirder fit at 2025-08-03 16:22:04.935 with tau around 30. Clearly there's some uncaught economy mode going on here.

![[Pasted image 20260520180451.png]]

![[Pasted image 20260520180922.png]]

The problem is in the df here: 

![[Pasted image 20260520181715.png]]

These are cycles which somehow didn't play despite DynEco not being triggered. I guess there's any number of reasons this could happen.

If I take out those rows, the fit looks fine:

![[Pasted image 20260520182543.png]]
# Absolute Changes in the Flat-Tops

- The absolute changes to the flat-top field are confined to roughly 2-4 Gauss
- Notable flat periods, although with a upward trend close to YETS - notable dip again at start of May
- Rolling median was window of 10

![[Pasted image 20260520164139.png]]


Looking at the interface at 2026-05-01 18:23:13.335, the issue is that the last SFT before the interface was especially high compared to those on the surrounding interfaces:

![[Pasted image 20260520184831.png]]

which may have somehow been caused by economy modes occurring before the interface...

![[Pasted image 20260520184742.png]]

The one at 2026-04-20 07:10:44.535 was clearly affected by a trim:

![[Pasted image 20260520185321.png]]

(surprisingly, the tau is still consistent with the median...)

# Double Exponential

- The fits look pretty good with a double exponential decay, with taus ~=3,35
- Difficult to get the upper tau but maybe this would be better with some smoothing

![[Pasted image 20260521121632.png]]

![[Screenshot_20260521_121826.png]]



*![[Pasted image 20260521135453.png]]*