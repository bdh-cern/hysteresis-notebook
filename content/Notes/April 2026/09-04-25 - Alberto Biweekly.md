
- Updated Alberto on issues with SHiP and with Panos' analysis of 2025/2026 chroma

# Dipole Measurements - full/flat MD1

- Lab measurement on MBB
- Two SCs: 
	- 20x full MD1->SFTPRO->LHC
	- 20x flat MD1->SFTPRO->LHC
- 20x MD1 is to reach accommodation (reproducible minor hysteresis loop)
- 10x LHC after each SC change to precycle as well
- MD1 and SFTPRO both had to be extended at idle current for ~20BP to fit with RMS restrictions on the power supply (HOLEC)
	- Removes eddies -> effect on hysteresis compared to machine experience. Even static hysteresis will be effected as eddies change the minor loop
- Measured five points: before SFTPRO, SFTPRO flat-top, before LHC, LHC flat-top, after LHC+ 1 more (?)
	- Flat-tops had to be discarded as they were too short for good measurements with rotating coils, and in SFT case the current is not static anyway
- Used two rotating coils: one in fringe field region, another in body region of MBB
- Findings:
	- -50e-6 T delta in B1 fringe field when comparing full->flat
	- +1.5e-6 T delta in B3 body field for same comparison
- Want to show that the settings difference qualitatively corresponds to these values (or rather, the signs on these values)
	- Make some plots/screenshots for magnets guys
- Aside: main bending field varies +- 1e-4 over length of dipole
- Do eddies really make the whole system non-static? They change the minor loop and complicate things in that manner, but does this not eventually get to a steady state over time, such that the eddy-effected minor loop at e.g. the start of an SFT injection will always be the same?

![[Pasted image 20260409161354.png]]
# NMR status

- Took inventory of NMRs and likely status before LS3
- Current measurement capability:
	- B-train static coil: integrated field
	- B-train NMR: the old NMR in the B-train. This resets the integration drift. Not sure if reset is done on the rising or falling edge - ask Matthias. 4.686108MHz (from looking at equipment, not sure what field this is).
	- New NMR #1: To be used for absolute measurement in the low field range (calibrated for 4e-3 to 116e-3 T). Abishek using this for R&D; likely not possible to get much data from it before LS3
	- New NMR #2: Can be used for absolute measurement in the high field range (0.7 to 3T). This never locks because the flat-top is too short. Not sure the use of this.
	- +5 dead old B-train NMRs. These remains will be properly put to rest during LS3.

# The Mystery of the Tau

- Some confusion over various eddy time-constants since I joined.
- Disagreement between lab and machine experience.
- There were two known eddy components:
	- $\tau_1 \simeq 10ms$ from 'lamination currents'
	- $\tau_2 \simeq 400ms$ from 'end plates'
	- ...and now a possible third component $\tau_3 \simeq 1s$ which is consistent with Anton's experience.
- The reason $\tau_3$ was not earlier identified is that measurement of eddies are sensitive to measurement parameters such as resolution/binning, measurement time etc.
	- Measurement time in particular is an issue as one should measure over $5\tau$ (i.e. 5s; longer than the SFTPRO flat-top) which which 3BP (from squinting at vistar)
	- Low resolution can cause separate components to be washed together, causing an apparent time constant which is longer than the sum of the separate components (e.g. a 50ms and a 400ms can look like a single 500ms component)