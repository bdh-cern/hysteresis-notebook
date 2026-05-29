
Template for downloading these:

```
from nxcals.api.extraction.data.builders import ParameterDataQuery

data_query = (
ParameterDataQuery.builder(spark)
.system("CMW")
.parameterEq("Device/Property")
.timeWindow(start_time, end_time)
.build()
)

data=data_query.select(Variable)

# or:

data_query = DataQuery.getForVariables(
spark=spark,
system="CMW",
start_time=start_time,
end_time=end_time,
variables=[list of DEVICE:PROPERTY:VARIABLE],
field_aliases={"OLD_NAME": "new_name"},
)

```

| Device/Property                      | Variable(s)                            | Timber Variable           | Description                                                                                                                                                                                                                                                   |
| ------------------------------------ | -------------------------------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BPMALPS_1/Orbit                      | positions                              |                           | The orbit data (offset from centre of tube) from BPMs in the first sextant of the SPS. There is also BPMALPS_2, \_3, etc.                                                                                                                                     |
| UCAP.SA.RevFreq-ACQ.1kHz/Acquisition | value                                  |                           | Revolution frequency in the SPS, sampled at 1kHz.                                                                                                                                                                                                             |
| SPS.BCTDC24.51454/Acquisition        | totalIntensity, totalIntensityInjected |                           | Intensity data from BCT. There are several BCTs; this is only one of them ('SPS DC-BCT SYSTEM A')<br><br>'totalIntensity' is the full signal (a vector).<br>'totalIntensityInjected' is one number representing the total intensity that was put into the SPS |
| BCTECO:Acquisition                   | ecoTriggered                           |                           | Flag indicating if DYNECO was triggered for a given cyclestamp                                                                                                                                                                                                |
| SPS.BQ.CONT:ContinuousAcquisition    | rawDataH, rawDataV                     |                           | Raw data from the BBQs. This is 'continuous acquisition' in that it does not come binned, but as a continuous signal per cyclestamp.                                                                                                                          |
| SPS:NXCALS_FUNDAMENTAL               | SUPERCYCLE_NB<br>                      |                           | Fundamental - seemingly not on CCDE.<br><br>SUPERCYCLE_NB is a unique key given to every new SC. Can use this to detect SC changes.                                                                                                                           |
| SPSQC:SPILL.QUALITY                  | effSpillLength                         | SPSQC:EFF_SPILL_LENGHT    | {sic} The effective spill length in ms. I'm guessing this is something like the 'if the extracted intensity had come from a perfect spill, how long would that spill have had to have lasted?'                                                                |
| SR.BMEAS-B-ST:CycleSamples           | samples                                |                           | B-train field in Gauss                                                                                                                                                                                                                                        |
| SPS.T2:Acquisition                   | intensityNotNormalized                 |                           | The un-normalised intensity which reaches the target (passes down?) T2. Also exists for T4 and T6 at least.                                                                                                                                                   |
| SPSQC:T2.INTENSITY.PERFORMANCE       | targetIntensityReference               |                           | The intensity that is meant to reach the target.<br><br>There is also targetIntensity, though this is broken                                                                                                                                                  |
|                                      |                                        | FDED_011_TT11101_AL.POSST | Seems to be the temperature of the cooling water on return from the SPS main bending magnets in C. Note that this is on WINCCOA, not CMW (Description: "PROBLEME TEMPERATURE RETOUR EAU DEMI MAIN MAGNET")                                                    |
| SPS:LOG.I.REF                        | value                                  | RPPEL.BA3.MBI/LOG.I.REF   |                                                                                                                                                                                                                                                               |


