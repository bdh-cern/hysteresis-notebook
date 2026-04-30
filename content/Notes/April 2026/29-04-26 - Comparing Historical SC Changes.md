
- Wrote some scripts to identify SC changes and compute the delta of beam parameters before/after
- Similar to Panos' work analysing the tune shifts over SC changes

# Spill Quality Factor

- On initial analysis, we do seem to be losing more spill quality factor (effSpillLength) on both SC transitions

![[Pasted image 20260429102827.png]]

![[Pasted image 20260429103411.png]]

# Replicating Panos' QH Analysis

My results are roughly consistent with Panos' so it looks like the scripts are working.

2025:

![[Pasted image 20260429114024.png]]![[Pasted image 20260429114038.png]]
2026:

![[Pasted image 20260429114654.png]]

![[Pasted image 20260429114725.png]]

NB these are Panos' plots from the CodiMD before my suggested tweaks, but everything will be the same OoM.

# Spill Sharing (T2 Only)

Found two interesting variables: the intensity and the target intensity. For T2, these are:

SPSQC/T2.INTENSITY.PERFORMANCE#targetIntensityReference
SPS.T2/Acquisition#intensityNotNormalized

There is also SPSQC/T2.INTENSITY.PERFORMANCE#targetIntensity, though this is broken.

I guess 'target' is the fixed target, i.e. not the target for what the intensity should be.


![[Pasted image 20260429160241.png]]

For T2 only:

![[Pasted image 20260429173434.png]]![[Pasted image 20260429173609.png]]

# Spill Sharing - RMS Intensity Error

- I calculated difference in RMS normalised intensity error across each SC interface
	- Normalised Intensity Error (NIE) is (measuredIntensity-referenceIntensity)/referenceIntensity 
	- RMS is the NIE for each T-line squared, summed, and rooted:
	$$RMS_{NIE} = \sqrt{NIE_{T2}^2 + NIE_{T4}^2+ NIE_{T6}^2}$$
	- So if all intensities are 100% off their reference, then the RMS NIE will be 3.
- Visible increase in the RMS from 2025 to 2026. Roughly 2x for both types of interface (pure->LHC or LHC->pure).

![[Pasted image 20260430103430.png]]
![[Pasted image 20260430103442.png]]

# Sharing Drift

- After the SC interface, I computed the drift of the intensity error
- This I did by taking the intensity error of the first cycle after the SC, then finding the maximum **positive** change from this within the next 6 SCs (presuming that if an operator made a trim in this period, this would make it better, not worse)
- Noteable increase in drift in 2026

2025:

![[Pasted image 20260430131829.png]]

2026:

![[Pasted image 20260430131706.png]]





