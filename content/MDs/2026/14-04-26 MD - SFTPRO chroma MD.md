
- Stephane trimmed momentum and Imains for a nice flat orbit near 0
- Now trimming tune
	- Lovely straight tunes in H and V
- Injection oscillated compensated
- 50Hz compensated
- Measuring with damper off

# SFTPRO-APERTURE

- First trim 16:24:02 
- Restored to dpp=0: 16:45:23
- Timing user LHCMD4

# SFTPRO-ZERO-APERTURE

- Before corrections, very high orbit (+5mm)
	- Probably because of the corrections we made for the previous SC
	- So this would imply that the dipole eddies have decayed over the ZERO and now the field is much lower
	- A ZERO is 1.2s so this points to the 300ms time-constant eddy that Alberto sees
	- Consequently, the tune decay seen last time ([[18-03-26 MD - SHiP with TSU Issues]]) is probably because of Alberto's (hypothesised) 1000ms time-constant

- Trimmed momentum to get it nice and flat at +5mm
- Then trimmed IMAINS to move the flat orbit down to ~0mm
- Tune trim to get it straight as well
- First trim: 17:14:03
- Restored to dpp=0: 17:36:34

# SFTPRO-ZERO-ZERO-APERTURE

- With 2 zeros, we have a +1.5mm orbit offset
- Small tune adjustments
- Tune looks fine, implying that the B2 eddies have already have already decayed by after 1 ZERO (because there wasn't any further decay between 1 and 2 ZEROs).
- Was really difficult to get flat orbit. Complicated by FGC failure. Now there with negative momentum correction
- First trim: 18:29:14
- Restored to dpp=0: 18:53:00
- Looking at AutoQ results, I wonder if the decay of chroma over beam time is indicative of the 1000ms eddy that Alberto described?

# SFTPRO-MD1-APERTURE

- Using flat 26GeV MD1, of course :)
- Small tune and momentum corrections
- First trim: 19:19:45
- Restored to dpp=0: 19:46:36

# Analysis

- Comparing the complete evolution of the tune components after the SFTPRO, there's a general upward trend in the chroma
	- Can't compare the tune curves over different cycles as these were corrected for

![[Pasted image 20260421150900.png]]![[Pasted image 20260421150906.png]]![[Pasted image 20260421150912.png]]

The decay does indeed seem to be consistent with the 1s time-constant decay Alberto mentioned:

![[Pasted image 20260421162749.png]]![[Pasted image 20260423140721.png]]![[Pasted image 20260423140725.png]]