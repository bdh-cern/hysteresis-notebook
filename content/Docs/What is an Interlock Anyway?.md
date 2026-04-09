
The Beam Interlock System (BIS) is a safety system that automatically dumps the beam if a fault is detected in a certain set of accelerator systems.

In the context of the SPS and LHC, this works in a hierarchical structure. At the bottoms are 'users', which are low-level systems like power convertors or [[Dumping the Beam (BAGs, BETS & TSUs)|TSUs]]. These produce 'permits' which are essentially Boolean signals representing their operational status. 

The permits are collected in bundles by 'Beam Interlock Controller Manager' (CIBM) boards[^1][^2]. Each manager board can handle up to 14 users (although this number will be increased after LS3). The manager board produces its own signal which is TRUE if all its user permits are TRUE, and FALSE otherwise.

The manager boards are then integrated into the 'beam permit loop'. This is a fibre-optic signal which runs along the ring of the accelerator[^3]. The manager boards act as relays for this signal. Provided all user permits for a given manager board are TRUE, the manager receives and propagates the frequency along the ring. If any permits are FALSE, the board stops its propagation, causing the permit loop to collapse around the ring. This triggers an automatic beam dump.

![[Pasted image 20260408110602.png]]
# Sources

Johnson, Roland, Christophe Martin, Tomasz Podzorny, Iván Romera, Raffaello Secondo, and Jan Uythoven. ‘The Consolidation of the CERN Beam Interlock System’. _Proceedings of the 12th International Particle Accelerator Conference_ IPAC2021 (2021): 4 pages, 0.767 MB. PDF, 4 pages, 0.767 MB. [https://doi.org/10.18429/JACOW-IPAC2021-WEPAB282](https://doi.org/10.18429/JACOW-IPAC2021-WEPAB282).

[^1]: Not sure how the reponsibilities of the CIBMs are divided.

[^2]: In fact, there is an intermediate Beam Interlock Controller User (CIBU) board, although this is not structurally important.

[^3]: For redundancy, there are actually two signals (path A and path B). They have slightly different frequencies.
