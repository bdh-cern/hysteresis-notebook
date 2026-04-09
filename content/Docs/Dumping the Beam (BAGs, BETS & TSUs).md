
# Summary

The TSU (Trigger Synchronisation Unit) synchronises the beam dump requests with the 'Beam Abort Gap' (BAG).

The BAG is a particle-free gap in the beam. This is in place so the kicker magnets can ramp up to the dump-kick energy over the particle-free period without prematurely affecting the beam.

![[Pasted image 20260407165605.png]]

Tthe TSU ensures that the kickers are ramped over the BAG. The failure of this synchronisation would likely result in major damage to the machine as parts of the beam are deflected into the vessel walls.

# Arming the TSU

Arming the TSU is relatively complex as it is has a circular dependency on the BIS. For the BIS itself, see [[What is an Interlock Anyway?]]
## Ring BIS

When the Ring BIS is established, the TSU permit to the BIS is forced to TRUE. This enables the Ring BIS to establish the permit loop. Subsequently, the TSU observes the permit loop and performs self-assessment. If either come back 'bad', the TSU permit to the BIS becomes false. [^1]

![[Pasted image 20260407170421.png]]

# Injection BIS

The Injection BIS arming sequence is identical to the Ring version, except that the permit is not initially forced to TRUE. Instead, the TSU permit only becomes TRUE at the end of the arming sequence. [^2]

Notably, the beam revolution frequency must be 'stable' (no spurious jumps, between certain extrema) for 450ms before injection for the permit to be TRUE (i.e. for injection to be permitted).
# The Beam Energy Transfer System (BETS)

The BETS is another system which binds the deflection strength of the kicker magnets to the energy of the beam such that, if triggered, they will ramp to the right energy and thus kick the beam onto the correct dumping trajectory.

The BETS is also a user and client of the TSU. The BETS permit is only issuable to the TSU 91ms after the ramp from 13[^3] to 26 GeV because this is the time required for the kicker magnets to charge to the latter energy. Only after this, energy tracking can commence.

# Sources

[EDMS #2738576 - Arming sequence for SPS Beam Dump System (SBDS)](https://edms.cern.ch/ui/#!master/navigator/document?D:101100275:101100275:subDocs)

Barlow, R. A., P. Bobbio, E. Carlier, G. Gräwer, N. Voumard, and R. Gjelsvik. _The Beam Energy Tracking System of the LHC Beam Dumping System_. n.d.


[^1]: Does this cause a dump?

[^2]: This is unclear. Need more information.

[^3]: Surely this is 13.5GeV? - number from EDMS
