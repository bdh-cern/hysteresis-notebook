---
aliases:
  - Radial Loop
  - Synchro Loop
  - Phase Loop
---
# References
[P.Baudrenghien, Low-Level RF](control_loops.pdf)
[Arthur Spierer, OP Shutdown Lectures: RF Beam Control](shutdown_lectures_rf_beam_control.pdf)


# Oscillations

The various control loops are intended to correct certain types of oscillations:

**Dipole Oscillations**: Oscillations of the (longitudinal) phase of the centre of the bunch around the stable phase. This is caused by an energy error from an injector to the receiving machine.

![[Pasted image 20260818153716.png]]

**Quadrupole Oscillations**: Each bunch has a non-zero length. At time of injection, the particles are following (longitudinal) phase-space trajectories defined by the injector, which inevitably have a mismatch with those of the receiving machine. This is because of differences in RF voltages between the machines. The result is a procession around phase space and then 'filimentation', which causes an increase in emittance.

![[Pasted image 20260818154221.png]]

# Phase Loop

The phase loop is designed to damp the dipole oscillation of the bunch. It does this by changing the RF phase and frequency to 'jump the bucket onto the injected bunch'. 

The phase loop is important to combat the effect of RF noise, which is important in storage rings where bunches may be held for several hours.

The phase loop conserves the longitudinal emittance (i.e. it stops the bunch from lengthening) but cannot keep the beam centred. We need the radial and synchro-loops for this. These loops are more 'gentle' so that the phase loop is still the ultimate authority on the beam. They are 'adiabatic', meaning here that the variation of the synchrotron frequency in one synchrotron period is small.

# Radial Loop

The radial loop slowly adjusts the beam energy (i.e. revolution frequency) via the RF in order to keep the beam centred.

The radial loop can only increase the beam energy. Any reduction is provided by the phase loop. Typically, if a beam is injected with a phase and energy error, the phase loop will first jump the RF phase and frequency onto the bunch, preventing blow-up. Then, the radial loop will slowly push the RF frequency (i.e. energy) up, driving the beam back to the centre orbit.

The radial loop is important around transition. This is because of singularities which appear in the beam frequency equations around this point; relying on a control loop instead of trying to analytically determine the transition frequency is the only option. In other words, a small frequency error here results in a very large orbital displacement, so one gives up on working out the frequency and just controls the orbit instead. 

The radial loop is important for fixed-target beams, as the SPS crosses transition during the ramp. However, beams destined for the LHC are injected into the SPS above transition, so the radial loop isn't required.

# Synchro-Loop

The synchro-loop keeps the RF frequency 'softly' locked onto a synthetic frequency. The synchro-loop is required during machine-machine transfer, as the buckets of the injecting and receiving machines must be coordinated.

The synchro-loop is primarily useful for SPS->LHC beams, because the frequency of the SPS must be very closely matched with that of the LHC for successful capture. In this case, the synthetic frequenct is that of the LHC. When the LHC sends this to the SPS, and the synchro-loop adjusts accordingly, the SPS orbits are violently adjusted to adapt to the new frequency. This is called 'rephasing'.

# Interaction of the Loops

![[Pasted image 20260819093643.png]]

The loop settings are handled by the RF APP ALL app in the CCM. Here, one can find the timings for the activation of the loops as well as numerous other settings.

When switching switching between synchro to radial (or vice-versa), there is an inevitable discontinuity in target frequency. This can be mitigated by blending between the two loops. In the case of switching from synchro to radial specifically, the initial radial offset is 'hidden' from the radial loop with an offset which slowly ramps down. This is all dealt with according to the 'Radial and Synchro Loop Toggling' settings in RF APP ALL (Loops tab -> Expert Settings). 

![[Pasted image 20260819095216.png]]

# Timings

In the below, one can see the timings for SFTPRO1: Phase loop and synchro-loop are enabled at the start of the cycle (SIX.MC-CTML), then the radial loop is started 30ms before the start of the ramp (SX.ST-RAMP-CTML), and only disabled at the end of the cycle (SX.BEAM-OUT-CTML). The phase loop is never disabled. The synchro-loop presumably turns off when the radial loop is activated, despite the SynchroLoopDisable setting being timed to beam-out as well. There is an unused segment in the top-right which appears to be used for enabling the synchro-loop a second time (i.e going synchro->radial->synchro).

![[Pasted image 20260819095922.png]]

