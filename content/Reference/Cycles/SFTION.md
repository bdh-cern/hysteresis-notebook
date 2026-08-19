# Basics

- 21 BPs long
	- 725ms beamtime/cycletime offset
	- 4 injections
	- FT is 13970-23056ms with slow ramp
- Flat-top at ~1.7T
- Seemingly a COSE slow extraction, much like SFTPRO
- AutoSpill corrects on momentum, like on SFTPRO (**presumably**)
- Sends Pb to the north area
- Chris: magnetic resonances in the PS switchyard cause momentum distribution variation

# Hysteresis Effects 

- The extraction does not seem to be majorly effected by [[Slow Hysteresis Drift]].
	- E.g. below, the FT field changes by the usual 3.5G (like with LHC->SFTPRO) but no obvious effect on the spill duty factor
	- Typical duty factor seems to be around 40% (as opposed to >90% for SFTPRO)
	- Experiments likely don't care so much about the uniformity of the beam
- Based on analysis of the below plots, the spill likely suffers from some sort of [Karenina principle](https://en.wikipedia.org/wiki/Anna_Karenina_principle).
	- The max duty factor is about 40%. Variations between 30-40% are common.
	- A perturbation in the field, and thus in the spill shape, can result a different bad spill shape with 40% duty factor.
	- This is opposed to an SFTPRO spill which is almost a perfect straight line. Any change in the spill shape will then reduce the duty factor.
	- Given that the mathematical definition of the [[Effective Spill Length]] is normalised to the total extracted intensity, its variation would suggest a variation in the momentum profile (for example) of the beam.
- In general, the beam is very inconsistent with a +-10% intensity variation shot-to-shot. It's probably quite difficult to do any analysis using it.
- Spoke to Chris and Martin:
	- Martin said that it would be difficult to get anywhere close to 100% duty-factor.
	- The users don't care so much about the spill quality, in contrast to SFTPRO. This is because of the difference in how the beam is used. For SFTION, the ions coming out of the SPS are the primary beam that will be studied/used by the users, whereas the SFTPRO beam is used to generate a secondary beam at the targets. The conversion of primary to secondary beam during SFTPRO means that the spill quality / uniformity is much more important (for whatever reason).
	- Chris told me that the +-10% intensity variation is a result of how the ions are generated.
	- We're not sure where the momentum profile variation comes from (if indeed it exists). The intensity effects are supposedly meagre enough that the intensity variation cannot be blamed.

![[Pasted image 20260805141110.png]]

Here one can see a slight decrease of the duty factor, although it later rises again with no obvious adjustments.

![[Pasted image 20260805142133.png]]

Below appears to be a fully-commissioned beam from 2025, with good sharing accuracy. Still no decay in the duty factor.

![[Pasted image 20260805142718.png]]

Looking at the BCT data on timber, the spill does actually move about a fair bit after the SC change. It appears to get flatter quickly, then it bounces around in a thick band.

![[Pasted image 20260805151225.png]]

![[Pasted image 20260805151632.png]]

In general, the beam is really inconsistent:

![[Pasted image 20260805152221.png]]


