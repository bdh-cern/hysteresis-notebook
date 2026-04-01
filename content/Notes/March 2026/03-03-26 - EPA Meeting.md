- AqFlow deployed on
	- KFA71 (kicker?)
	- PS RF caivities monitoring
	- MKP spark detection
- In teach case, aqflow captures data based on a subscrtipion, performs analysis of anomalies, and outputs notifications (e.g. on mattermost or email)
- Add errors to chroma measurement tables
- Quantify the settings changes in numbers for IPP
- Matthias proposes setting up a synthetic B-train for hystersis quantification
	- This would consist of taking B measurements for every possible SC for 10-20 repetitions or so
	- Each SC would require a seperate measurement for each possible preceeding SC
	- However this would not take into account dynamic economy, because this can happen anywhere and makes the history completely dynamic
- The NMR probes can correct the drift on the B-train system by pegging the B-field to an absolute value
	- There might be problems with the LHC injection plateau because this is too long and there might be significant drift over its course 
		- Why can't we try for 2 NMR locks over this plateau? - maybe we can
- Are the ramp-downs different per cycle? Eddies are only dependent on dI/dt, so hypothetically the static hysteresis effecting the beginning/end points of the ramps aren't an issue, but if the ramp speed differs, then there could be a problem
- For DynEco or even LHC cycles without a long flat top, the eddies on the ramp up will never fully decay, meaning that the expected top-field is never reached, this then effects the static hysteresis for the next cycle.

# Rampdowns

The cycles I downloaded were:

- sftpro: SFT_PRO_MTE_East_extraction_L4780_2026_V1
- lhcinj: LHC_4inh_BCMS_Q20_2026_V1
- ihcindiv: LHC_INDIV_1inj_Q20_2026_V1
- lhcinj: LHC_4inj_BCMS_Q20_2026_V1
- lhcion: LHC_ION_3inj_Early_Pb82_Q26_2025_V1
- lhcpilot: LHC_PILOT_Q20_2026_V1
- awake: AWAKE_Q20_2025_V1
- hiradmatpilot: HIRADMAT_PILOT_L8400_Q20_2025_V1
- hiradmatinj: Hiradmat_4Inj_Q20_2025_V1
- sftship: MD_SHiP_L1230_East_Extraction_2026 MD18163

Having plotted these on the one axis, the profiles are appreciably different. The main feature is a bump between 400 and 1000ms which appears in all cycles with varying geometry.

The rampdowns also end at different seperations from the end of the BP, which will obviously influence how many eddies are left on the subsequent cycle.

![[Pasted image 20260305144202.png]]
