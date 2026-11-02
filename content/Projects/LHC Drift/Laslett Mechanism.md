Started from [[21-10-26 - MMM]].

# Summary

A Laslett correction is only applied to the quads when a.) it's an LHC multi-injection cycle and b.) the beam is injected (and only from the second injection on). This makes it a good candidate for the mystery noise mechanism.

The correction is stored as a discrete variable in LSA (QF/REF.EVENT_TRIM.STEPS) which is then added (invisibly) to QF/I_REF. To see the 'actual' reference current, one needs to download the I_REF of the power-convertors (QF/LOG.I#REF - NB there is an identical variable called RPPAG.BA3.SQF:I_REF). 

![[Pasted image 20261022114411.png]]

Here one can see that the noise only starts when the injections differ (injection 1 okay both time, injection 2 only succeeds on blue line):

![[Pasted image 20261022113912.png]]

![[Pasted image 20261022132120.png]]
# Issues

On the 16th of July, there is a single cycle where the Laslett correction was applied even when the beam wasn't in. 

It still appears as if the trend of the B-train changes here. If so, this would invalidate the hypothesis.

![[Pasted image 20261021165058.png]]

Quite strong evidence now from the exceptional no-beam, fully-corrected cycles that the Laslett is not the issue:

![[Pasted image 20261021173530.png]]

It also seems to be the case that there are cases with no beam, correction, and differing drifts. This would imply that it's the not beam presence either. So it's likely that there's another timed mechanism that's causing this.

![[Pasted image 20261022112012.png]]
\