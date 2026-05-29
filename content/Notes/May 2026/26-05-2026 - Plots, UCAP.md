- Weird MD2, MD1 after LHCION today. Why?
-
![[Pasted image 20260526110823.png]]

# Plots

![[Pasted image 20260526123955.png]]
- B: two-tau decay, as expected, nice fit
- Temperature: starts increasing BEFORE SC interface. Very odd.
- Spill quality: takes a hit for about 4-5 minutes, then restored
- Sharing error: quick decay (\~2mins) then drifts up slowly
- Measured I: no pattern at all. Then again, this is only for the power converter in BA3
- Orbit: decay corresponds to that of B-field
- **28-05-26:** discovered that I QF wasn't plotting correctly. It's not the same as I MBI (as shown in these plots)

**Realised that I was using the wrong T**

- With the correct T, there is a clear increase in temperature (of the return water from the MBIs)

![[Pasted image 20260526132105.png]]However, if I look at the wider scope, this is actually a rise out of a relative low:

![[Pasted image 20260526132336.png]]

- Is this seen on other 'nice' interfaces?
- Does the double-tau decay hold over long periods of time
- Could the effects of the eddies on the static hysteresis be causing the long decay rather than the temperature?

# Other interfaces

- Looking at 26-04-14 (which I'd marked as 'weird') there is actually now a pretty clear trend in the current which corresponds to an increase in temperature
- Spill and sharing qualities were actually already pretty bad beforehand. 
	- Sharing qualities has very obvious decay after interface - spill quality goes up a bit

![[Pasted image 20260526163502.png]]

- Here, the temperature had been quite strange in the vicinity (although remains constant overnight -- presumably staying on SFT SC) The temperature increase is about the same as the other interface (35 to 42 degrees).
![[Pasted image 20260526165716.png]]
- The 'really weird one' from 25-08-03 (the weirdness turned out to be because of some dropped cycles even though DynEco wasn't playing) also has this funny trend in T and a long disruption of the normalised sharing error which corresponds to an apparent beam-out period, over which there must have been a momentum trim
![[Pasted image 20260526164725.png]]
- Again we have this weird drop and increase again. I wonder if the whole LHC filling cycle is in that drop?
- Also noticed that the 2025 interfaces have chaotic current before/after, whereas there's a very clear decay in the current in the 2026 interfaces, even though they have similar temperature changes 
	- Small changes (range \~0.14 A with the trend, in 2026 \~0.07 A without the trend in 2025 )
	- I wonder if this is something that wouldn't be accounted for in the B-train? Is it water cooled as well? Could we be seeing the wrong fields because the magnets are different temperatures?
		- If not cooled, is it possible that the long B-train trends we see in 2025 were in fact not occurring in the ring magnets, but now that something has changed and the temperature is possibly not being compensated correctly (hence the decreasing ring currents in 2026), this long trend has now been introduced to the ring magnets?

![[Pasted image 20260526165234.png]]

- Interface at 26-05-01: same story as before

![[Pasted image 20260526170228.png]]![[Pasted image 20260526170434.png]]


# To do

- [x]  Set up UCAP
- [ ] Email Jani Lehtinen
- [x] Look at several other individual interfaces
	- [ ] Show some more for 2025
- [ ] Run fits for whole year
- [ ] Plot temperature with labelled SCs
- [x] Get calibration function
	- [ ] plot 'hysteretic B' (measured B minus that expected from measured current)
- [ ] Work out what the expected change in field from the change in temperature is
- [ ] Sync this notebook
- [x] Plot programmed current

# Programmed current

- Programmed current decreases after SC interface in 2026:

![[Pasted image 20260528134709.png]]

- But not in 2025:

![[Pasted image 20260528135327.png]]

- This is a trim applied by the operators to recover the spill. There is also a trim applied to QH.