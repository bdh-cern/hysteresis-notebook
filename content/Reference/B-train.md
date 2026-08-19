'The' B-train is one of several magnetic measurement systems at several accelerators. Here we are concerned with the SPS B-train.

The system consists of two above-ground dipoles connected in parallel with the SPS dipoles such that they replicate the field given by the 'actual' dipoles at a given current. 

## Things to Note

- The B-train has a precision of about 1e-5 T.
- The operational B-train does not currently (05-02-26) have a NMR system for integration drift correction
	- Despite this, there is still an m1BCorrection field for the operational B-train
- If the FCGs are off, the usual B-train devices will publish simulated values instead of real measured ones.
- 'Bdot' is used to refer to $\dot{B}$, i.e. the rate of change of $B$ with time.
	- Bdot is really the only thing the RF team cares about because it drives the $\dot{p}$ during acceleration. Integration drift on the operational B-train is therefore irrelevant to them.

# Drift Correction

- B-train uses an NMR set to 0.11 T to perform correction of the integration drift of the fixed coil measurement.
- This correction happens on all cycles (MD1, LHC, SFTPRO, etc).
- For each cycle a time-window is defined where this field strength is expected to be found. If/when the field moves through the value during the window, the measurement is re-zeroed (or more precisely, reset to 0.11 T).
- The correction usually occurs right before injection, but for SFTPRO it in fact occurs right **after** injection, at the start of the ramp.
- There is an app to track the drift correction [here](https://wrap.cern.ch/app/207860)

Example of the LHC marker window (the end of the window is presumably just the end of the chart):

![[Pasted image 20260410134029.png]]


## Important Variables

| Variable Name                                | Unit  | Description                                                                                 |
| -------------------------------------------- | ----- | ------------------------------------------------------------------------------------------- |
| SR.BMEAS-OP-B-SD:SamplesFromTrigger:samples  | G (?) | The operational B-train measurements for the SPS. Not drift corrected.                      |
| SR.BMEAS-SP-B-SD:SamplesFromTrigger:samples  | G (?) | The spare B-train measurements for the SPS. Note that the 'spare' is the drift-corrected B. |
| SR.BMEAS-OP:BtrainStatus:btrainData          |       | Flag for real (0) or simulated data (1) for operational B-train                             |
| SR.BMEAS-SP:BtrainStatus:btrainData.         |       | Flag for real (0) or simulated data (1) for spare B-train                                   |
| SR.BMEAS-SP:MarkerAcquisition:m1BCorrection  | G     | The last correction applied by the the NMR system on the spare B-train                      |
| SR.BMEAS-SP:MarkerAcquisition:m1MarkerBLevel | G     | The 'level' at which the NMR correction above was applied (don't know what this means)      |
|                                              |       |                                                                                             |

# Limitations

There are various different B-train variables in NXCALs, all of which seem to have a different 'treatment' of the underlying data.

The most reliable variable for absolute measurements of the field seems to be SR.BMEAS-SP-B-SD:SamplesFromTrigger. However, the drift correction seems to cause artefacts (see [[Dodgy Drifts]]) which can limit its usefulness for analysing the [[Slow Hysteresis Drift]].

![[Pasted image 20260703162739.png]]

This variable also has an offset from the programmed B in LSA. This could be because of any number of things, such as bad calibration between B and I in LSA or between I and B in the B-train fluxmeter. It's likely that the actual field is neither that reported by the B-train nor that programmed in LSA.

The B-train/LSA offset is about 120-140G and seems to be relatively constant over the course of months.

![[Pasted image 20260703162840.png]]


# Pics

![[Pasted image 20260409162721.png]]

![[Pasted image 20260409162702.png]]

![[Pasted image 20260409162730.png]]

![[Pasted image 20260409162740.png]]