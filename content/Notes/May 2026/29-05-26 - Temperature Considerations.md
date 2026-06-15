
- Observation about temperature:
	- Flat-tops experience a long decay when going from LHC SC to SFT SC.
	- The temperature is increasing, the field is going down with a decay constant of 20-30 cycles.
	- When going from SFT SC to LHC SC, temperature decreases. But the field does NOT go up. There is only a short 'decay' upwards to the full field strength.
	- This is a symmetric problem: the temperature goes from 41 C, to 35, to 41. If the transition from 35->41 causes such a noticeable downwards decay, then 41->35 should cause the same decay in reverse (a noticeable upwards decay).
- Much more likely then that the long drift is because of accumulating eddies. These wouldn't cause a decay at the SFT->LHC interfaces, because the LHC cycles are saturating the magnets and dominating the history. Near saturation, dB/dI -> 0, so the eddies are negligible in this region (some other possible explanations). But with SFTPRO only, the eddies can have a cumulative effect over many cycles.  
- Need to plot the flat-top fields during LHC SC alongside temperature to verify
- Below plots occured 2026-22-03 00:30:00.000

****

![[Pasted image 20260611123036.png]]

![[Pasted image 20260529160936.png]]
![[Pasted image 20260526132105.png]]

- The decay is not visible for the SFT->LHC transition:
	![[Pasted image 20260603120211.png]]
![[Pasted image 20260610104753.png]]


****

Plotting the various interfaces, it looks like the flat-top decay continue even after the machine is off for extended periods...

![[Pasted image 20260610151555.png]]

For the above, had some beam issues although I can't see if it was off:

![[Pasted image 20260610151853.png]]

![[Pasted image 20260610151907.png]]

The magnets are cycling in these blank segments; the issue seems to be with the B-train itself. It makes a difference whether I get CycleSamples or SamplesFromTrigger:

![[Pasted image 20260610164651.png]]![[Pasted image 20260611122939.png]]