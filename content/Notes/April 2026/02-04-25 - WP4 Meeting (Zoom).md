- Last MD, analysis
- Flat top hysteresis compensation
- Underlying predictors are operationally unusable
	- Trained without MD1
	- Not generalised
	- Large number (>166)
	- We could develop the GUI and the UCAP infrastructure with the presumption that we can slot in a working model
	- Meeting with Anton week after next to take inventory of all of his work before he leaves
	- Questionable usefulness in fully testing this solution as it likely won't work and we risk souring the operators on this idea

# MDs

- [[18-03-26 MD - SHiP with TSU Issues | MD on the 18th]] revealed that SHiP -> MD4 has issues
	- Couldn't get a TSU permit for the MD4 to be injected after SHiP cycle
	- Concern that this means you couldn't have a physics cycle right after SHiP
	- However later validation allowed a permit to be generated for SFTPRO-SHiP SC
	- This points to a settings problem, i.e. that there is some issue with the timing in the settings of the measurement cycle MD4
	- This was validated later in the week -> now need to talk to Stephane to fix this
- Tirsi later did an MD which was able to clear the permit (SFT->SHiP->MD1) which implies that there is no issue with SHiP specifically (although they didn't end up injecting beam)

# Chroma

- Panos has done some[ analysis showing the delta Q in the SFT injection plateau](https://codimd.web.cern.ch/N7QQQ_VeQmCwJvShVtODmw#) when the SPS switches between SFTPRO+LHC and just SFTPRO supercycles over time
- The 2025 data are relatively stable at deltaQ=0.1
- The 2026 data show a larger delta of ~0.15 (and increasing so far)
- Want to do this again and analyse how dynamic economy influences this (presumably just 1 DynEco cycle as it is rare to have multiple in a row?)
- Also want to look at how the spill quality factor changes on flat top
- Since the flat top is trimmed, we will have to only use the first few flat tops before the operators react to the delta and mitigate it
- Need to look into this and do this analysis myself, ask Panos for help/access, details of how he did this chroma analysis

![[Pasted image 20260402155154.png]]
![[Pasted image 20260402155059.png]]


# Other
- Need to ask Alberto and Abishek about the status of the NMR now to see if we can get data for a new predictor
- Otherwise, we want to hold off on the GUI etc until we have everything else square