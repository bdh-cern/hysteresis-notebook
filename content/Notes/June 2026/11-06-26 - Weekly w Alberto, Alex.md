- Double check beam on SFTPRO3 during magnets segment of MD
- Plot the flat-top field diff over last year
- Overlay B-train after SFTPRO during LHC fill and pure SFT SCs
- Presented idea about temperature decay - agreed that it is less likely that the temperature is causing this long decay after the LHC->SFT interface
- Slides found at
- Accidentally testing the UCAP device by leaving it on on the HYSTCOMP-TEST node, which apparently has authority to trim BHYS (despite this seemingly being impossible from the base HYSTCOMP node last Wednesday: [[03-06-26 - Parallel]])
- BHYS increased to +0.02T, which I find suspicious because usually one would expect a negative correction. Have to compare this to way was actually being played, because I think this was SFTPRO coming off HIRADMT, and I don't know what that interface looks like.
- Discussed the accidental test [[12-06-2026 'MD' - Accidental Testing]]
- Flag for if the correction is active which is published and can be displayed in the GUI
- Check to make sure the spare isn't being played
****

The flat-top when switching to LHC filling is at a consistent field over time:

![[Pasted image 20260612170328.png]]

Note that the script for this plot didn't take into account trims. Had to do some manual cleaning of data that was polluted by economy modes.

****

**After Weekend**

Contact UCAP support to get access to logs
Fit decays over whole year - account for trims