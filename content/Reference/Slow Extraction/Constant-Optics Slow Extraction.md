
COSE (Constant-Optics Slow Extraction) is a method of performing the slow extraction of the SPS beam by keeping the optical strengths constant and instead performing a momentum sweep to push particles into the 2/3 integer tune resonance.

# Pre-COSE

Before COSE, the beam was extracted with a tune sweep. In other words, the quadrupoles were modified in order to bring the tune of the beam close to the resonance and extract. The change in tune meant that the extraction sextupoles also had to be altered, which in turn meant that the separatrix rotated over the time of the extraction, which is a proxy for the particle momentum. As a result, particles with higher dp/p had a greater x'. This caused higher losses and degraded extraction quality. See [[Slow Extraction - Basics]] for more details.

# COSE

In COSE, the momentum of the beam is increased, which pushes the beam into the resonance via the chromaticity (of -1). We want to keep the optics constant, i.e. all $k_n$ n-pole strengths the same. From the equations discussed in [[Beam Physics - General Concepts]], we know that the strength of an n-pole is:

$$k_n = \frac{e}{p}\frac{\delta^n B}{\delta x^ n}$$

and thus for protons:

$$k_n \cdot p(t) =\frac{\delta^n B(t)}{\delta x^ n} \propto I (t)$$

So the current on each n-pole will increase linearly with the momentum when we perform the sweep, and the n-pole strength will stay constant. As a result, the virtual sextupole is kept constant, and the separatrix does not move during extraction.

# Up or Down?

Not sure about the below figure. It states that the beam rigidity is increased to push towards the extraction (which is indeed what happens). However, it shows the waiting stack at a higher rigidity than the resonant one. If this diagram were to be believed, clearly one would have to in fact lower the rigidity to lower the stack into the resonance.

![[Pasted image 20260819123615.png]]