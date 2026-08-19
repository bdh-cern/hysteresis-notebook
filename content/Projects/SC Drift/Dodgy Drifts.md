Looking at strange drift profiles which my data cleaning isn't detecting for whatever reason.

More detail in [[Slow Hysteresis Drift]]

| Start               | End                 | Plot                                 |
| ------------------- | ------------------- | ------------------------------------ |
| 2023-07-17 00:02:46 | 2023-07-17 04:25:34 | ![[Pasted image 20260703115921.png]] |
If I plot this in my main script, I get:

![[Pasted image 20260703122003.png]]

So it looks like there is actually a long period of NaNs which isn't discovered by the analysis script.

I checked both SamplesFromTrigger and CycleSamples, but no visible difference.

I identified an oversight in the data collection (a .limit before an .orderBy, which gave a degree of non-determinism and cut random data)

![[Pasted image 20260703131120.png]]

Now that the plot makes sense and IMEAS is constant, I wonder if this dip is a B-train artefact:

![[Pasted image 20260703161451.png]]

There's a ~-2.5G correction on the NMR at the same time as the dip in B. The fact that the effSpillLength and sharing error are unchanged implies that indeed nothing is actually going on with the real B-field.