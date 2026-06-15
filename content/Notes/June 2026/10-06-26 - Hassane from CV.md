- Talked to Hassane Sabri from CV about the temperature.
- Related to [[29-05-26 - Temperature Considerations]] and maybe [[(Plan) 02-06-26 - Temperature MD]]
- The temperatures of the magnets are not measured. The cooling loop works by running cooled, demineralised water from the BA (access buildings?) on the surface down to the magnets, then measuring the temperature of the return and increasing the flow the if temperature increases.
- Each BA serves two sextants of the ring (with separate loops? this is how I drew the diagram than Hassane confirmed but not sure it makes much sense)
- B-train is connected to BA3 loop
- BA3 exhibits unusually high temperatures compared to other BAs, by a few degrees.
- Also a separate cooling loop for the transfer lines
- Not sure if introducing a few zeroes would have temperature effect
- Talk to Philip Schwarz for more info on magnet cooling
****
- Get access to winccoa temperature monitoring
- Change temperature variable in analysis to BA3 (compare to other BAs?)
****
 
![[Pasted image 20260610120326.png]]

FDED 21 11 10  12

21 - seems unrelated
11 - not high enough (max 38 deg ish)
10 - could be (41 deg)
12 - this is it. Runs high at 46 degrees. BA3 mentioned in various descriptions. 

| Field             | Value                                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Variable name** | `FDED_012_TT50001.POSST`                                                                                            |
| **Description**   | "Transmetteur de temperature retour primaire eau brute - PIW142" (return primary raw-water temperature transmitter) |
| **Unit**          | °C                                                                                                                  |
| **System**        | WINCCOA                                                                                                             |
