Also on the 16th

- Last-minute opportunity to test the drift corrector during a SHiP MD.
- As of 1040, the SC is SFTPRO2, MD5, MD1, SFTPRO2, MD5, MD1
- Both SFTPRO2 and MD5 are SHiP cycles (albeit slightly different)
	- Apparently, they will later change to extract on MD5 
- Extraction only occurring on SFTPRO2.
- Can't perform tests here.:
	- The SHiP FT is only 1BP, and from experience the incorporation time should be about .5s after the FT start, which means here it would cause a fast ramp over the course of the FT and probably ruin the spill
	- Speaking of, the spill is already extremely messy with effSpillLength~=800ms. It's very possible that correcting the spill would not work as expected
	- The hysteresis is completely flat, so there isn't actually any drift to correct anyway, just a static offset (the removal of which would probably require a lot of trims in order to restore the beam)


![[Pasted image 20260715110134.png]]
- Updated UCAP node to hysterpid 2.7.0, with B-offset functionality etc.
- Noticed that in historical decays, the QF trims needed to make a nice consistent spill length could also be a triple exponential if you squint 
	![[Pasted image 20260715111823.png]]

# Later

- Spoke to Dwane, who suggested changing the device config to specifically target SFTPRO1
	- This is now done. v2.7.2 now.
- Watching the SHiP MD, which is actually playing SFTPRO1 and doing something with the steering. Here it's quite visible how DynEco pulls the dipoles down to a lower hysteresis mode during the period at 1455ish when they were switching eco on/off.
- Acquisition property with trim message (showing logs essentially)

![[Pasted image 20260715173909.png]]

# More write-up here

- Weird note: sharing error increased when they switched to longer flat-bottom (HIRADMAT1 -> HIRADMAT2)
To do after holiday:
- hysteresis GUI
- adding a tune plot to the time-series plots above
- testing after SC change with tune trim
- GUI for latest trims published to SPS
- Small NN hysteresis predictor
- Instructions for SPS OP