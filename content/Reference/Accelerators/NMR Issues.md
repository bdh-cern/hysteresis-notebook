
The drift-correcting NMR in the B-train has a few issues. I first noticed these whilst I was looking at outlying instances of the slow hysteresis drifts (see [[Dodgy Drifts]]). Now, they have become an issue for the hysteresis predictor. Note here I am looking almost exclusively at SFTPRO1 (and MD1, as we shall see).

Usually, the NMR correction should be <1G, but during glitches it will reach several G.


# Types of Glitch

The NMR correction seems to fail in a few different ways:

### Correction Cloning

Occasionally, SFTPRO1's NMR correction snaps up to become identical to that of the preceeding MD1 (to the last decimal place). This happens both for isolated cycles and for long series of >50 MD1/SFTPRO1 pairs.

The field drifts here, even though the correction does not. There is no supercycle change here either. 

Questions: 

- Why is the field changing so much without an SC change?
- Why does this cause SFTPRO to latch to the MD1 correction?
	- Does the trigger field now occur outside the trigger window, losing it?

![[Pasted image 20260915111638.png]]
### NMR Shifts

Other times, the level of all correction appears to change for several hours. The corrections do not shift by the same amount. Note that the fields here are taken at the flat-top, which is well after the NMR correction.

![[Pasted image 20260914171037.png]]


### Correction Drift

Note that the NMR correction trends upwards over time. This is not an issue with the NMR per se --- rather the coil measurements are probably getting more noisy as the other components of the B-train degrade.

![[Pasted image 20260914171053.png]]

# Trends in NMR Glitches

![[Pasted image 20260915171842.png]]

Note the log scale on all axes.

Most cloning episodes are individual events, although some last for many tens of cycles:

![[Pasted image 20260915174905.png]] 

# No Injection Hysteresis

![[Pasted image 20261013153509.png]]![[Pasted image 20261013153519.png]]![[Pasted image 20261013153559.png]]