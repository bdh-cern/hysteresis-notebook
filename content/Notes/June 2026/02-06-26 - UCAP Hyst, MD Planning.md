
- The BHYS parameter is set up in an awkward way
	- BHYS 'inline' with B and IMAINS - ideally, B and BHYS would be summed going into IMAINS instead
	- The target of BHYS is set to whatever B is, so corrections then need to be applied on the *correction* value of BHYS
- Need to get a solid value for the fast decay constant --- this can stand in for actual measurements if a DynEco fires (despite the fact that a DynEco will change the decay constant... hopefully it's approx okay)
- 

![[Pasted image 20260602115602.png]]
![[Pasted image 20260602115624.png]]

- Actually it's good on NEXT:
![[Pasted image 20260602145859.png]]

-  The [B2Current make-rule](https://gitlab.cern.ch/acc-co/inca/lsa/-/blob/develop/lsa-ext-sps/src/main/java/cern/lsa/ext/sps/trim/rules/makerule/B2CurrMakeRule.java?ref_type=heads) make rule doesn't work for this hierarchy since it scans for parents of the IMAINS node which are of parameter type 'B'. This was once the case for BHYS, but it has since been moved to its own parameter type (called BHYS also). As such, trims to BHYS on LSA are completely ignored by IMAINS. 
- There's also the issue that the Bs have to be summed before converting to I via the calibration function, whereas this set-up, at the very best, does B->I and BHYS->I and sums the current, which won't work as B->I is not a linear relationship in this region.
	- Looks like the behaviour of the hierarchy is indeed such that the node performs a summation over its inputs/parents.
	- For the quads, we have a similar structure:
	![[Pasted image 20260602153527.png]]
	- Each of these arrows (make-rules) outputs a current, so I presume that the IMAINS node just sums up each input and stores that as its canonical value.
	- The lower make-rule just copies over IMAINS ('parent') to IREF given certain checks pass. So the summation isn't happening there.
- Need to make decisions on the incorporation rule but I think DELTA_IR should be fine.
![[Pasted image 20260602162351.png]]

- ToDos:
	- Make a plan for temperature experiments
	- Implement safeguards on absolute B
		- Examine the LSA trim history for approximate range
	- Graph for absolute flat-top field over the last year+
	- Meeting with Michi tomorrow (opts: Michael, Kevin)
	- Email Jani/Carlo/Alberto about temperature


- Flat-top Bs look like this: 
	![[Pasted image 20260603102432.png]]
	- This is for ...L4780_2026_V1 