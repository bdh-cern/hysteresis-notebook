- Late follow-on from [[10-02-26 - Kevin, Michi, Michael]]
- Discussed also in [[02-06-26 - UCAP Hyst, MD Planning]]

# Hierarchies

- Hierarchy for the BHYS parameter in NEXT looks like this![[Pasted image 20260603095109.png]]
- Doesn't work because the B2Curr make rule (both in-arrows to IMAINS) scans for parent parameters of type B, takes only one, then uses that to get the appropriate I via a calibration function
	- Note BHYS is not of parameter type B, but of type BHYS
- We need it to sum both B and BHYS before calibrating I.
- Solutions:
	- Don't have BHYS. Just use the correction of B.
	- Have B and BHYS summed to some node called 'BMAINS' which is then used with B2Curr to get IMAINS
- In PRO, the hierarchy looks like this:![[Pasted image 20260603095548.png]]
- We need this to match the NEXT hierarchy.

# Incorporation Rules

- On next, there's an incorporation rule for B using a backwards/forwards DELTA_IR.
	- Possible issue that DELTA_IR is not robust against changes to the ramp, which is well-calibrated.
- We think this should probably be CONSTANT_DECAY_IR. The expected behaviour is that trims sent to the flat-top BHYS will automatically create a control point at the very end of the ramp, so that the flat-top change does not propagate back beyond it.
- This is what I've put in NEXT now:
	![[Pasted image 20260603102009.png]]
- Is this correct? Not sure how the CONSTANT_DECAY_IR is meant to work (is it absolute or relative to start of BP)

