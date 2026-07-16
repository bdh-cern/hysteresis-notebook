
- Got the following error whilst testing UCAP on next:
	![[Pasted image 20260619165538.png]]

- Important parts: TrimException, Limit exceeded for MBI in relevant BP, Acceleration out of limits at X=2.884, acc=88669.44, maxAcc=66666.0
- Looking at makerule...
	- The actual SpsIMainsToIRefMakeRule only catches specific TrimExceptions and throws the general one
	- I'm guessing checkMinMaxLimit or checkCurrentLimits threw the acceleration exception
		- checkAccelerationLimit is indeed within checkCurrentLimits
- Will change the incorporation time and hopefully this will be nicer
	- Indeed it is
****

- For the first time, the trims are working nicely. Currently BHYS is bouncing around -0.00025 T (2.5G)
- I notice that the noise of the B-train is enough to cause noise in BHYS
	- Probably some way of smoothing this, but would likely involve an exponential fit
- The BHYS has accumulated to 5G, which is too much (should currently be 0.8Gish)
	- I think this is an effect of running on NEXT
	- Yep:
	$$\begin{split} \Delta &= BMEAS - BREF \\ \Delta&= BREF + err - BREF \\ \Delta &= err \\ BHYS + \Delta &= BHYS + err\end{split}$$
	- So this is just going to accumulate forever. Turning it off and trimming back to 0.
	- I guess I could make this better for NEXT by doing an absolute trim of bhys_prog + bhys_change every time, rather than assuming that the trims are actually doing anything
	![[Pasted image 20260622152714.png]]
	