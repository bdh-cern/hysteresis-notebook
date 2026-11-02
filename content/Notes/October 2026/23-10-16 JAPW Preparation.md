
- Quentin (?) doesn't like constant trimming
- Ideal would be to send the trim to a FESA class instead of via LSA, which would stop certain signals from being blocked
	- 'Sending forward control to the FGCs'
- Real-time control in-place in the SPS FGCs (i.e. the mechanism which lets us circumvent using LSA)
- End of LS3: field-feedback control hopefully in place in FGCs
	- However, the B-train is also not that reliable - partly because of the length of SPS cycles compared to e.g. PS, which allows integrator drift to accumulate.
	- Drift is a larger issue with LHC cycles than SFTPRO1 (see [[Noise Observations]])
	- Maybe we could request some MD time at the start of run 4 to test the B-train control on SFTPRO1 specifically