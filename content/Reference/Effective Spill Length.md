
The effective spill length (units: ms) is a measure of the spill quality, generally used in the context of SPS slow extraction (SFTPRO1).

It is logged as SPSQC:SPILL.QUALITY#effSpillLength in NXCALs and referred to as SPSQC:EFF_SPILL_LENGHT (sic) on Timber.

According to [Kain et al. IPAC, 2017](https://cds.cern.ch/record/2289708/files/mopik049.pdf), it is calculated via:
$$
t_{\textrm{eff}} = \frac{(\int{I(t) dt})^2}{\int{I(t)^2 dt}}
$$
where $I(t)$ is the extracted intensity as a function of time.

If $I(t)$ is a constant (constant intensity - a perfect spill), then we get $t_\textrm{eff}=t$, i.e. the effective spill length equals the actual spill length.

In general, the $\int{I(t)^2 dt}$ denominator punishes unevenness in the spill. To understand this, imagine a spill with an overshoot and an undershoot in $I(t)$, and another perfect spill. The same amount of particles are extracted in both overall. Compared to that of the perfect spill, the numerator of the imperfect spill will be unchanged, because the same number of particles are extracted and this number is then squared. However, the denominator will be increased, because the positive contribution of the squared overshoot increases the integrand by more than the squared undershoot decreases it. Thus for any 'wobble' in the spill rate, the effective spill rate is decreased.