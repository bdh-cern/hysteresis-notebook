
- Discussed MD plan with Alex and Michael
- Some confusion over the beam in the LHC - whether this is needed. Alex points out that if the intention is to quantify the RF noise, then it is useless, because the RF cavities will be on anyway for the cycle. But Abhishek also wanted to use it to look at the orbit drift during injection too. - verified Abhishek does not need to do this
- Kevin is making clones of the operational cycle, so I will have to check whether the following properties are being logged for the relevant timing users:
	- SPSQC:SPILL.QUALITY - SPS.USER.ALL                 
	- SR.BMEAS-B-ST:CycleSamples - SPS.USER.ALL
	- SPSQC:T{2,4,6}.INTENSITY.PERFORMANCE - SPS.USER.ALL
	- SPS.T{2,4,6}:Acquisition - SPS.USER.SFT*
- I should make a utility script that downloads and displays the relevant properties for a given time-frame.
- LHC is indeed LHCINDIV with 4 injections
- Continued [[05-05-26 - MD Planning]]

# Email sent to group

(The following contains Alex's adjustments.)

Hi everyone,

Here is the plan for Wednesday's MD as it exists thus far. Let me know if you have any suggestions.

**Part 1: B-train/NMR calibration (13:00 - 15:00)**

The magnets team would like to calibrate the NMR/B-train relationship by taking clean measurements on both instruments at the same time.

Supercycles:

SC1: SFTPRO - MD1 - CALIBRATION
SC2: SFTPRO - LHC - MD1 - CALIBRATION

These should be played 50xSC1 -> 50xSC2 -> 50xSC1. There should not be any beam (one exception; see below). Importantly, there must not be any trims made to the dipole field on any cycle.

'CALIBRATION' will be a 10BP, 26GeV cycle, _completely flat_ on the dipole field. This means it can have no corrections on momentum, B, IMAINS, etc.

'LHC' will be an LHCINDIV with a long flat-bottom. During SC2, it will be played ca. 25 times without beam and ca. 25 with beam. 

Process:

Just waiting as the data is collected in NXCALs.

  
**Part 2: Hysteresis (15:00 - 18:00)**

During this part we want to quantify changes to the flat-top properties after a change in SC and apply an appropriate trim.

Supercycles:

SC3: SFTPRO - MD1 - SFTPRO - MD1 - SFTPRO - MD1
SC4: SFTPRO - LHC - MD1

I believe LHC will be an INDIV as well in this case. All cycles will be clones of operational cycles for safety when trimming. We will have beam in the SFTPROs and LHCs.

The SCs will be played SC3 -> SC4 -> SC3 -> SC4 -> SC3.

Process:

We will run SC3 for a while and then switch to SC4. At the point of the switch, we will grab the flat-top properties and observe the decay to the regime of the new SC (especially effective spill length, flat-top B, and sharing quality if possible). We will run SC4 for a while, then switch SC4->SC3 and do the same. 

After running SC3 for another while, we will switch to SC3->SC4 again and immediately apply a trim on BHYS which corrects for the property changes we measured for that switch. Hopefully, as the machine settles into SC4, the properties will return to good values. We then repeat this for the SC4->SC3 switch as well.


Best,

Brendan