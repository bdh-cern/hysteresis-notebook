See write-up in [[Testing Drift Corrector - Write Up]].

- Also on the 16th
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

# Actual Test
- After the MD was finished, I turned on the compensator and made sure it behaved as expected.
- No corrections were applied initially as the field was already at acceptable levels.
- Dwane played a single LHC SC at about 18:57, which immediately pushed the magnets to the hysteretic state
- Moved back to SFT. The compensator fixed the drift
	- There was still a loss alarm, although usually this happens several times after SC change, and this time it only happened once.
- I observed that the effSpillLength drifted and sharing error improved and held steady
	- This is the contrary of in [[06-05-26 MD - Magnetic Calibration, Flat-top Studies]]. There, in the static case of the LHC SC, we saw that the dipole correction fixed the spill length properly but not the sharing factor.
- When we tried with SFT->LHC in the MD, the effSpillLength was fixed and the sharing error was still off
- When we look at a normal LHC->SFT change, both factors drift
- Weird note: sharing error increased when they switched to longer flat-bottom (HIRADMAT1 -> HIRADMAT2)

![[Pasted image 20260730120640.png]]

# Tune Considerations

![[Pasted image 20260730122253.png]]

Looking at 400-900ms in beam time on the tunes (thus not measured in the same place as the reference time etc):

![[Pasted image 20260730160557.png]]

Then for the start of the FT (4260-4460ms I think) - (strange periodicity on QH):

![[Pasted image 20260730161146.png]]

This is because there's a very static peak at 0.65 visible in the playback. This might be because of the damper, although we presumed this was off. In any case the tune measurements after the debunching (at start of FT) are useless.

![[Pasted image 20260730173343.png]]

Looking at the end of the ramp (4150 - 4250ms) you can actually see the tune changes:

![[Pasted image 20260730173132.png]]

During the run with Dwane, we can see that the tune is actually corrected for by the compensator as well. So why does he still have to make FT tune trims?

![[Pasted image 20260730173631.png]]

The QF I trims don't seem to have any effect on the actual tune in either case. Checked - this makes sense because they only play with the tune later:

![[Pasted image 20260730161611.png]]

![[sftpro1_reference_points.png]]