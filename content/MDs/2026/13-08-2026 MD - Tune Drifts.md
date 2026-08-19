# Motivation

The purpose of this MD was to investigate the change in tune which occurs when switching between an SFT-like and LHC-like supercycle, and vice-versa.

We had the kick on to get a nice clean tune reading, and the dipole hysteresis compensator active on the flat-top so that we could observed only the quadrupolar hysteresis via the tune, without it being washed out by dipole/orbit effects.

# Info
- Start/end:
		2026-08-13 13:00:00.000000+02:00
		2026-08-13 15:30:00.000000+02:00
- Two supercycles:
	- SFTION1-SHIP-LHC3-MD1 (LHC-filling-like)
	- SFTION1-MD1-SHIP-MD1 (SFT-physics-like)
	- There were also some ZEROs in each
- We measured the tunes on the SHiP cycle (specifically MD_SHiP_L1230_Q26_S33_2026_LowInt)
- Hysteresis compensator configuration:

| Key                                | Value          |
| ---------------------------------- | -------------- |
| `trim_context`                     | `SPS.USER.MD5` |
| `max_bhys_change`                  | `1.0e-4`       |
| `min_bhys_change`                  | `0.1e-4`       |
| `max_corrected_b`                  | `1.8010`       |
| `min_corrected_b`                  | `1.7990`       |
| `flattop_reference_cycletime_ms`   | `5210`         |
| `start_of_correction_cycletime_ms` | `4800`         |
| `correction_factor`                | `0.8`          |
| `min_b_train_acceptable_value`     | `1.7`          |
| `max_b_train_acceptable_value`     | `1.9`          |
| `target_b`                         | `1.8138`       |
| `drive`                            | `true`         |
| `send_trim`                        | `true`         |

- Kick applied at 4440ms cycletime (4240ms beamtime)
- Start of FT is at 4460ms cycletime, thus compensator ramps between 4460-4800ms 

# Plots

- I chose the kick time poorly, but we can exploit the small difference in time between the kick start and the compensation start to look at the tune with the dipole compensation both on and off.
- There was some beam-out during the first few cycles of the SFT-like SC. This was some sort of interlock issue that Chris fixed. Unfortunately this means that it's difficult to see any fast decays (~4 cycles) which may have occurred in this region.
- In these plots, the orbit was retrieved from BPMALPS_6:LoggingAcquisition:logDataOrbitPosStartFlatTopH (thus this is the mean orbit at the start of the flat-top in sextant 6.)
- There were also numerous beam-out cycles after the switch back to the LHC-like SC due to some losses in the PS.
- The dipoles seemed noisy after the switch back to the LHC-like SC. I don't know why this is, but I don't think it's a usual magnetic effect. Could be a hardware issue etc, or could be something that the MD team was changing.
- I initially observed some strange behaviour of the tune whilst using nafflib. Using an FFT instead resolved this. The old analysis is below.
- For the FFT analysis, I employed a temporal filter which took into account the likely scale of tune changes from cycle to cycle. The max change was set to 0.001 usually, relaxing to 0.01 near SC interfaces. I chose these values based on sanity-check plots of individual BBQ slices. Using a tighter temporal filter (0.0005) does seem to clean up the data in H and shows a possible trend, but it results in nonsense behaviour in V, so the 0.001 has to stand as the tightest sensible filter for our resolution.
- The resolution of the FFT is about 0.00115, so details below that are lost. I padded with extra zeros to increase the bin resolution, and also used scipy detrend to get rid of any DC/linear component (although because of the mod calculus involved I don't think this would have made much difference). Also used a Hann window to reduce side-bands.

# Dipole Compensation On:

- Plot below has reference time 5210ms and tune measurement window 4800-4900ms (the 100ms after BHYS is fully applied)

![[Pasted image 20260818112131.png]]

- When switching to SFT-like, the tune changes by -0.002. There may be a slight decay afterwards (this would make sense, as neither SC saturates the quadrupoles).
- When switching back to LHC like, the tune seems to level out around 0.0005 lower than before. This may have been because of changes to the dipoles made by the MD team.

# Compensation Off

- Plot below has reference time 4265ms (mid-FT) and tune measurement window 4440-4460ms. This is right after the kick.
- The vertical tune is not reliable, since the vertical kick only occurs at 4480ms, 20ms after the compensation ramp happens.

![[Pasted image 20260818114355.png]]


- One can see the +0.005 change in QH that Francesco predicted (and which is in-line with the trims the operators have to make in this scenario).
- The tune change is very fast. This is not expected from pure quadrupole hysteresis, since they never saturate and thus should drift slowly each way. It also follows the dipole hysteresis, meaning that this could be a radial loop or feed-down effect:
	- Beam rigidity $B\rho = p$ tells us: bending field goes down -> radius increases -> radial loop must **reduce** p.
	- Reduced p gives reduced tune (chromaticity is +0.5 in LSA).
- With increased resolution, maybe we could see the slow component of the dipole drift in the tune signal
- The fast decay might have been visible in the portion at the start of SFT-like which was deleted by beam-out.

# Old Analysis (Bad Tune Acquisition)

##  Dipole compensation on:

- Plot below has reference time 5210ms and tune measurement window 4800-4900ms (the 100ms after BHYS is fully applied)

![[Pasted image 20260814171912.png]]


When the SFT-like supercycle plays, the tune jumps by approximately +0.02. When moving back to the LHC-like SC, the tune appears to move quickly back. However, it continues to drift slowly downwards, as does the MBI current (adjusted by the compensator). This implies that the dipoles are drifting  or the B-train is noisy for some reason, even though they are saturated during the LHC-like cycle.

## Dipole Compensation off



- Plot below has reference time 5210ms (mid-FT) and tune measurement window 4440-4480ms. This is right after the kick. It also overlaps with 20ms of the BHYS ramp (which starts at the start of FT, i.e. 4460ms), but the longer envelope turns out to help with tune acquisition more than the start of the BHYS ramp hinders it.

![[Pasted image 20260814174153.png]]

When switching to the SFT-like SC the tune appears to immediately jump by +0.02 as well. However, it then decays back down with a familiar triple-exponential shape. When switching back to the LHC-like SC, there may also be a small jump downwards.

I would guess that this is the interaction of the dipole and quadrupolar components:
- After the LHC cycle is removed, the minor loop changes quickly (a few cycles) and the quadrupolar field increases, raising the tune. I infer this from the fact that neither the SFT nor the LHC cycles saturate the quads, and the latter drives them to a lower current.
- However, the slow drift of the dipoles causes the tune to drift downwards again. I infer this from the fact that the decay looks so similar to the slow dipole drift. 
	- More information is required on the radial loop to understand how this works
- When the LHC cycle is re-introduced, the dipoles are immediately reset due to saturation, and the minor loop is quickly restored, therefore restoring the initial tune.

After I switched to using an FFT this looked much more sensible. In fact, they're so clean that one can now see the resolution of the BBQ.

![[Pasted image 20260817110802.png]]
## Tune in Ramp

- Plot below has reference time 4265ms (about 200ms before the end of the ramp) and tune measurement window 4265-4365ms.

![[Pasted image 20260814180748.png]]

- Here, the tune changes by about -0.04. This is what Francesco measured back in 2017 or so for a similar SC change. It also roughly corresponds to the tune trims the operators make when a similar SC change is made.
- The tune is immediately restored when switching back the LHC-like SC, which implies that this is primarily an effect of the dipole hysteresis.


![[13_aug_md.png]]


Kick at 13:19:

![[Pasted image 20260814163036.png]]

Kick at 13:23:

![[Pasted image 20260814162822.png]]

Kick at 13:45:

![[Pasted image 20260814162900.png]]

