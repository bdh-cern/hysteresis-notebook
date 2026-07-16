- Field change when moving between SFT physics -> LHC filling is instant
- When changing from LHC filling -> SFT physics there is a triple exponential decay
- Investigated this in [[06-05-26 MD - Magnetic Calibration, Flat-top Studies]]
- Fixing it with [[Drift Corrector]]

![[Pasted image 20260624111537.png]]

- Fit this decay across the clean interfaces I could find:
	- No trims
	- Limit on eco events
	- Enough LHCs before and enough SFTs after interface

![[Pasted image 20260618105048.png]]

- This drift is probably because of the cumulative effects of the eddy currents, which slowly change the extrema points of the cycle.
- See [[29-05-26 - Temperature Considerations]] for why it's probably not that.

![[Pasted image 20260611123036.png]]

![[Pasted image 20260625164846.png]]

# Correction

In order to correct this drift, we have to apply a delta to BHYS each cycle:
$$
\begin{align*}
\Delta &= \textrm{BMEAS} - \textrm{BTARGET} \\
&= \textrm{BREF} + hys + \textrm{BHYS} + sys - (\textrm{BREF} + sys) \\
\Delta &= hys + \textrm{BHYS} \\
\textrm{BHYS} - \Delta &= -hys \\
\end{align*}
$$
Where:
	- BMEAS is the measured field from the BTRAIN
	- BTARGET is the desired B
	- BREF is the programmed B (SPSBEAM/B)
	- BHYS is SPSBEAM/BHYS
	- *hys* is the field causes by hysteretic effects
	- *sys* is the systematic error between the B-train and the programmed B

# Source of BTARGET, AutoSpill

It's necessary to tie BTARGET to SPSBEAM/B (i.e. the actual programmed B in LSA) because other processes such as AutoSpill trim on this value. 

If BTARGET were a static value defined in the config, then if AutoSpill were to trim B (via MOMENTUM), the drift corrector would then 'correct' for this trim on the next cycle. 

However, we can't simply correct to the present value of SPSBEAM/B, as the [[B-train]] never agrees with this value. There is about a 130G offset between the two values that we can quantify and continuously adjust such that we correct to BTARGET = SPSBEAM/B + sys.

The offset doesn't change much over the months:

![[Pasted image 20260703161418.png]]