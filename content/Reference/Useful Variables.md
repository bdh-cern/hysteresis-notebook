
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
```

| Device/Property                      | Variable(s)                            | Description                                                                                                                                                                                                                                                   |
| ------------------------------------ | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BPMALPS_1/Orbit                      | positions                              | The orbit data (offset from centre of tube) from BPMs in the first sextant of the SPS. There is also BPMALPS_2, \_3, etc.                                                                                                                                     |
| UCAP.SA.RevFreq-ACQ.1kHz/Acquisition | value                                  | Revolution frequency in the SPS, sampled at 1kHz.                                                                                                                                                                                                             |
| SPS.BCTDC24.51454/Acquisition        | totalIntensity, totalIntensityInjected | Intensity data from BCT. There are several BCTs; this is only one of them ('SPS DC-BCT SYSTEM A')<br><br>'totalIntensity' is the full signal (a vector).<br>'totalIntensityInjected' is one number representing the total intensity that was put into the SPS |
| BCTECO:Acquisition                   | ecoTriggered                           | Flag indicating if DYNECO was triggered for a given cyclestamp                                                                                                                                                                                                |
| SPS.BQ.CONT:ContinuousAcquisition    | rawDataH, rawDataV                     | Raw data from the BBQs. This is 'continuous acquisition' in that it does not come binned, but as a continuous signal per cyclestamp.                                                                                                                          |
