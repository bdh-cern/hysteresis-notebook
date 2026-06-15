
# Problem

- There is a slow decay of the field after an LHC->SFT SC change.
- It was presumed that this was due to temperature increases. However, if this were the case, we would presumably see an increase of field when the temperature decreases at the start of the LHC SC, which is not present (see [[29-05-26 - Temperature Considerations]]).
- There are a couple of alternative explanations for this:
	- It's a cumulative effect from the eddies, which cause the static hysteresis to drift slowly by altering the field extrema seen by the magnets.
	- It's just what the static hysteresis accommodation looks like.
- Discussed possibility of experiment to test this during [[02-06-26 - UCAP Hyst, MD Planning]].


# Experiment

- Want an experiment/MD to show that this slow decay is not related to temperature.
- The slow decay is visible on the SFT SC, when the temperature increases. We'd want to control for temperature here and see if it still happens, but:
	- We can't just change the cooling loop
	- We could change the temperature by waiting a long time between cycles, but this would also change the eddies.
		- Would not eliminate them completely, since if we played one SFTPRO, waited a minute, then played the next, then the eddies would still alter the extremum at flat-top, if not that during the injection plateau.
- What we could do is add 2-3 ZEROS between each SFTPRO and MD1. 
	- This would probably allow the eddies to decay (as their largest component has a tau of about 1s (see [[09-04-25 - Alberto Biweekly]]).
	- Hopefully this small change to the timing would not alter the temperature curve too much. 