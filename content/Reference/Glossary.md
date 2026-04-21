
See also [[Abbreviations]]


### MD

'Machine Development'. Used in two contexts:

1. An MD session: A slot of time where we perform experiments on the machine in order to improve machine performance (as opposed to generating data for physics).
2. One of several magnetic cycles, typically called MD1, MD2, etc. These are magnetic cycles which are not intended to produce physics data but rather serve some other purpose in the running of the machine (e.g. MD1 which is intended to lessen hysteresis effects).

### PPM

'Pulse-to-Pulse Modification'. The ability or act of modifying each pulse in a supercycle in an independent, dynamic manner. Also 'PPM-ness', which also refers to the ability or capacity of being able to do so.

## Flattening/depowering MD1

![[Pasted image 20260115113047.png]]

Flattening or depowering MD1 means replacing the current cycle with zeros, i.e. simply running the idle current of the machine for the same amount of time. This is distinct from 'removing' MD1, which would entail actually removing it from the schedule (such that one has, e.g., two SFTPROs 'touching' each other with nothing inbetween).

Depowering MD1 thus saves power, but not time.

### JAPC

'Java API for Parameter Control'. A framework for controlling machines with Java. Needed to get e.g. the real-time IREF from the control software in order to perform hysteresis prediction.

Confluence: https://confluence.cern.ch/spaces/JAPC/pages/410005394/Home

## LXPLUS

Linux service for AFS.

# AFS

Andrew File System. The old file system which is now largely surplanted by EOS.

# TSU

Trigger Synchronisation Unit. Synchronises beam dump requests with the Beam Abort Gap (BAG) upon request from clients such as the interlock system.

![[Pasted image 20260407160253.png]]

# BAG 

Beam Abort Gap. A gap in the beam which allows the dump kicker to rise to full power.

![[Pasted image 20260407153258.png]]

The kicker rises as the gap passes so that it is already at full field by the time the next particles arrive. The beam thus experiences a constant dumping kick.

# Interlock

Genereally the Beam Interlock System (BIS). A hierarchical system which automatically dumps the beam if a fault is detected in the operation of the accelerator.

# MKB

Dilution kicker magnet. There are vertical and horizontal versions (MKBV, MKBH). These are kicker magnets which sweep the beam over the target to dilute the energy received at any one point.

# BETS

[[Beam Energy Tracking System (BETS)]]. A component of the dumping system(s). The BETS binds the deflection strength of the kicker magnets to the energy of the beam such that, if triggered, they will ramp to the right energy and thus kick the beam onto the correct dumping trajectory.

