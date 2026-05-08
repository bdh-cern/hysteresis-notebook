
- Need to ask Theo for clone names
- Need to tell operators what we want to do
	- Chris and Johan
- Ask for SFT clone to specifically go in SFT* timing user
- Any operational MTE beam on SFT clone, the operational INDIV on LHC_INDIV_4Inj_Q20_2026_Meas_Magnet, no beam on MD_26_L12000_Q20_2026_V1
- Upstream machines can supply whatever beams they like to facilitate this, deliberately do not include beams in these machines to avoid confusion
- See [[06-05-26 MD - Magnetic Calibration, Flat-top Studies]]

Remarks for ASM, sent also to Chris and Johan:

Cycles required in the SPS:

MD_26_L1685_Q20_2026_V1
MD_26_L12000_Q20_2026_V1
LHC_INDIV_4Inj_Q20_2026_Meas_Magnet
SFT_PRO_MTE_East_extraction_L4780_2026_V2_Clone - Please make sure this remains mapped to an SFT* user so that the data is correctly logged to NXCALs

The MD will consist of 4 BCDs:

**BCD1**: SFT_PRO_MTE_East_extraction_L4780_2026_V2_Clone - MD_26_L1685_Q20_2026_V1 - MD_26_L12000_Q20_2026_V1
**BCD2**: SFT_PRO_MTE_East_extraction_L4780_2026_V2_Clone - LHC_INDIV_4Inj_Q20_2026_Meas_Magnet - MD_26_L1685_Q20_2026_V1 - MD_26_L12000_Q20_2026_V1
**BCD3**: SFT_PRO_MTE_East_extraction_L4780_2026_V2_Clone - MD_26_L1685_Q20_2026_V1 - SFT_PRO_MTE_East_extraction_L4780_2026_V2_Clone - MD_26_L1685_Q20_2026_V1 - SFT_PRO_MTE_East_extraction_L4780_2026_V2_Clone - MD_26_L1685_Q20_2026_V1
**BCD4**: SFT_PRO_MTE_East_extraction_L4780_2026_V2_Clone - LHC_INDIV_4Inj_Q20_2026_Meas_Magnet - MD_26_L1685_Q20_2026_V1

We want to play these in the order:

BCD1, BCD2, BCD1 (13:00 - 15:00)
BCD3, BCD4, BCD3, BCD4, BCD3 (15:00 - 18:00)

Beams: 
Any operational MTE beam for the SFT_PRO_MTE_East_extraction_L4780_2026_V2_Clone
Any operational LHCINDIV beam for LHC_INDIV_4Inj_Q20_2026_Meas_Magnet
No beams on MD_26_L1685_Q20_2026_V1 or MD_26_L12000_Q20_2026_V1

We will not need beam for BCD1.
During BC2, we will play LHC_INDIV_4Inj_Q20_2026_Meas_Magnet ~25 times without beam and ~25 times with beam.
During BCD3 and BCD4 we need the beam on both SFT_PRO_MTE_East_extraction_L4780_2026_V2_Clone and LHC_INDIV_4Inj_Q20_2026_Meas_Magnet

I have deliberately not included beams for the upstream machines as specifics don't matter to us here, so they should do whatever is easiest for them.

Other things:

BCD1 and BCD2 are intended for calibrating the B-train, so it's important that there are no trims applied to the dipole field whilst they are playing.

![[Pasted image 20260505151321.png]]