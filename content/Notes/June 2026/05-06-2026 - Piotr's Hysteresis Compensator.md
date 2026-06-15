- Trajectories into the PS from PSB
- Root: memory effect from extraction magnets
	- Worst in ring 2 because it has 2x the magnets of other rings
- Fixed with 0.3A added to bends for 2GeV cycles when preceded by 1.4GeV
- Simple feed-forward: look up correction based on current to magnets
	- Correction is 2D function in LSA
	- 3 different preceeding cycles
- FGCs are locked 900ms before injection based on a certain timing signal
	- The way this works out means only 300ms to send trim for next cycle
	![[Pasted image 20260605141503.png]]
- If cannot get previous cycle status, gets the same cycle from previous supercycle (provided checks e.g. the SC has not change in the meantime)
- They correct just on the current, not on e.g. the B
	- Note that we correct on BHYS now, which is different to B, because B trickles down to RF in the hierarchy as well, whereas BHYS ultimately just correction IMAINS
		![[Pasted image 20260605142637.png]]
- Difference from our approach is that this corrects subsequent cycles in the same SC whereas our corrector corrects the same cycle all the time but in different SCs.
- Kevin says that injection oscillations are corrected before every LHC fill, which means SPS does not notice issues
	- However, the LHC does actually see differences, even when these oscillations are corrected for.