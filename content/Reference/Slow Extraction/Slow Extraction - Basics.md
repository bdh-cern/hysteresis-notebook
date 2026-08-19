# Resonant Extraction

Cyclotrons and synchro-cyclotrons work with integer or half-integer resonances, which gives spills of ~ms. Synchrotrons use half-integer or third-integer resonances, with spills of ~s.

![[Pasted image 20260812115203.png]]

Particles in 1/3 resonance 'lock on' to the separatricies and move between them, gaining amplitude each time. This takes ~100 turns. The particles are then shaved off on the outer separatrix by the septum before they can impact the inner wall.

![[Pasted image 20260812120042.png]]

The particles have a orbital displacement of about 30mm before they are finally kicked into the extraction septum.

![[Pasted image 20260812125936.png]]
# Steinbach Diagrams

Steinbach diagrams illustrate the spill by plotting the 'waiting' beam and the resonating beam on axes of betatron amplitude against momentum offset ($\delta p / p$).

![[Pasted image 20260812123046.png]]

The red line delineates the unstable (resonant) region. As the beam is pushed in (it's unclear if the SPS still uses a betatron core for this), the particles are subjected to resonance and their amplitudes increase so that they can be extracted.

The spill gains momentum over time, since particles with the lowest momentum are extracted first. This is because the beam has negative chromaticity (-1); when the momentum is ramped, the tune of the beam decreases, moving the particles into the resonance from above[^1].

# Resonance Stop-band

The stop-band of the resonance is the tune range (around $1/3$) in which particles above a specific betatron amplitude $J$ are unstable. It is given by:

$$|\delta Q| = \sqrt{\frac{J}{24\sqrt{3}\pi}}|S|$$

where $|S|$ is the strength of the virtual sextupole. Note that $|\delta Q|=0 \implies J=0$, i.e. that there is no stable region for on-resonance particles. Likewise, without any sextupolar field, only perfectly-resonant particles are extracted (which is to say, none will be extracted).

# Sextupolar Driving, Virtual Sextupole

As demonstrated by the above equation for the stop-band, the tune-range captured by the resonance is dependent on the strength of the **virtual sextupole.**

The virtual sextupole is a mathematical construct which summarises the sextupolar effects during extraction. These effects come from the dedicated resonance sextupole and any other sextupolar errors from the machine (especially the dipoles).

Although there are other sextupoles in the SPS, these are intended to be used for chromaticity adjustment, and positioned to cause as little resonance excitation as possible. Meanwhile, the extraction sextuople is positioned in a zero-dispersion region so as not to disturb the chromaticity.

- How big of an impact does the dipoles' sextupole field have on this?

[^1]: Have to check this as I always thought it approached from below.
