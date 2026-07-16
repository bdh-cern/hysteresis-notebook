![[Pasted image 20260609140847.png]]

NB: on 25th July, discovered above was incorrect (note difference in flat-top field before/after the first LHC cycle) and have regenerated it using correct reference point and B-train variable:
![[md_6th_may_2026.png]]
****
- Change in main B gives change in spill quality
- Change in quads gives change in sharing error???
- After LHC->dyneco x 6->dyneco x 6->SFT, no decay in SFT. Really flat, lower than usual SFT
- But after LHC->dyneco x4 ->SFT, there was still a decay in SFT.
- Big drop is temperature effect? Slow drop is magnetic effect?
****

Cycles:

MD_26_L1685_Q20_2026_V1 (MD1)
MD_26_L12000_Q20_2026_V1 (MD5) (calibration cycle)
LHC_INDIV_4Inj_Q20_2026_Meas_Magnet (LHCMD1)
SFT_PRO_MTE_East_extraction_L4780_2026_V2_Clone (SFTPRO3) 
# Magnets Calibration

- Ran without issue.
- BCDs were: 
	- SC1: SFTPRO - MD1 - CALIBRATION
	- SC2: SFTPRO - LHC - MD1 - CALIBRATION
- Only played SC1 -> SC2 -> dyneco SC2 (not back again as planned)
- LHC was played both with and without beam
- Nice clean data taken
- On 07-05-2026, Carlo, Alberto and I discussed the noise on the B-train. Carlo thinks that the noise was reduced for all data taken. 
- Magnets was of the impression that the RF was playing on CALIBRATION, but this was most likely not the case. Will try to find some way to tell if RF was playing or not.

# Hysteresis

- BCDs were:
	- SC3: SFTPRO - MD1 - SFTPRO - MD1 - SFTPRO - MD1
	- SC4: SFTPRO - LHC - MD1
- 15:25 - Started with SC3 after a period of SC2 and then SC1 dyneco.  
	- Noted a very flat 2pole field from B-train.
	- Very flat spill quality
	- Sharing had a large decay towards reference.
- 16:00 - Switched to SC4. 
	- Spill and sharing deteriorated immediately. 
- 16:10 - Eyeballed The delta-B of the flat-top between SC3 and SC4. This was 3.5G or so. 
	- Applied this to the SC4 flat-top via BHYS 
	- Spill was immediately recovered (no decay)
	- Sharing was immediately improved (no decay)
- 16:30 - Removed the BHYS correction, and applied a equivalent MOMENTUM correction based on Francesco's advice that this would also trim quadrupoles, etc.
	- Sharing quality did not improve
	- Spill quality did improve moderately, but not to good levels
- Removed MOMENTUM correction and re-applied BHYS correction
- 16:50 - Applied a trim to QH
	- Very small delta (+0.002)
	- This was worked out from the 2pole correction: $$\Delta Q_H = Q_{H} \times \frac{\Delta B_{DIPOLE}}{B_{DIPOLE,SC1}}$$
	- ...i.e. the change in QH was proportional to the correction we applied to the dipole field.
	- I'm not convinced that the necessary QH corrections would be calculated so easily
	- Very minor improvement in sharing quality
	- Very minor improvement in spill quality
	- Possible that a larger change would much improve things.
- 17:00 - Changed the BHYS correction up to 4G. Improvement in sharing and spill.
- 17:05 - Removed BHYS correction
- 17:07 - Changed back to SC3
	- Observed long drift of sharing, spill (both improving over time)
- 17:35 - Switched to SC4
- 17:40 - Switched SC3 and turned on dyneco for 4 SFTPROs
	- Hope was that the dyneco cycles would 'fast-forward' the decay when returning to the full SC3. This was based on the very flat B-train seen at 15:25 which was also after two dyneco periods (about 12 cycles)
	- However, there was still long drift of sharing and spill
- 17:50 - Back to SC4.
	- Similar idea to before: dyneco but now on SC4, then change to SC3.
	- Still long drift of sharing and spill
## Some conclusions

- It may be possible to correct spills quality based only on dipole B
	- For SFT SC -> LHC SC, there isn't much drift, so this is a pretty simple correction
	- I can probably cook up a PID to apply such a correction for the long drift seen after an LHC -> SFT SC interface
- At 15:25, the B-train was flat, the spill quality was flat, but the sharing drifted significantly.
	- This implies that sharing is NOT only effected by dipole hysteresis
	- Sharing and spill can be somewhat decoupled
		- Sharing is effected by tune/dispersion even if orbit is correct
	- The dyneco that occured before SC3 would have let the dipoles relax. But dyneco does not play on quadrupoles (or higher). So when we switched back to full SC3, there would have been decays still occuring in quadrupoles. 
	- This would have been invisible to the B-train
	- Should still consider the effects of the quads in the sharing error
- The dyneco experiments towards the end of the MD showed that dyneco doesn't relax the dipoles quickly.
	- However, we should try again using a very low-energy SC (e.g. only MD1s)
	- It's possible that there are two drifts occuring: temperature and hysteretic accommodation
		- The extended dyneco could have allowed the magnets to cool quickly after SC2 at 15:25
		- Not worth speculating on this; will check the temperature data

![[Pasted image 20260508111044.png]]
![[Pasted image 20260507170224.png]]

![[Pasted image 20260507165708.png]]

## Weird MD1 SC

- Michael pointed out this strange SC sequence which was played on the 7th around 13:55 and again at 17:30 ([logbook1](https://be-op-logbook.web.cern.ch/elogbook-server/GET/showEventInLogbook/4548113) [logbook2](https://be-op-logbook.web.cern.ch/elogbook-server/GET/showEventInLogbook/4547955)) . Maybe I will ask the operators what this was for in case it's some sort of quasi-degauss... ![[weird_md1s.png]]

