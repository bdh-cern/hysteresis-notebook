Goal: establish a schema which describes the structure of the data-set. Specifically, the schema will describe the fields of each data-set entry, i.e. the information associated with each individual cycle.

# Open Questions

- What goes in each git branch
- What does the final processing script look like 
- How general do we want the dataset
- How do we build up the dataset?
	- Just categorisations first?
	- Or straight to full datasets with stored B, I

# Necessary Information


| Field                                 | Description                                                               | Data Type      |
| ------------------------------------- | ------------------------------------------------------------------------- | -------------- |
| Cyclestamp                            |                                                                           | int            |
| User                                  |                                                                           | str            |
| Cycle name                            |                                                                           | str            |
| Commit #                              | To identify which project version performed the categorisation            | str            |
| Real NMR correction                   | Identified by Matthias' linear-fit method                                 | float          |
| Real NMR correction time              | Ditto, in cycle-time                                                      | float or int   |
| NMR incidents                         | Classification of any NMR glitches apparent in NXCALs                     | list(str)      |
| B-train/LSA offset                    | Difference between the B-train-reported field and LSA programmed field    | float          |
| Laslett correction, QH                | 2D array with time/magnitude of Laslett corrections (only for LHC cycles) | (float, float) |
| Laslett correction, QV                | Ditto                                                                     | (float, float) |
| Time since last SC change             | Regard 'real' changes, e.g. if spares were played                         | int            |
| Time since last dyneco                | Do not include fulleco                                                    | int            |
| Cycles since SC change                | As above, measured in any played cycles                                   | int            |
| Cycles since last dyneco              | As above, measured in any played cycles                                   | int            |
| Full cycle played                     | If the full magnetic cycle was played                                     | bool           |
| Full beam injection                   | If the beam was fully injected                                            | bool           |
| DynEco                                | If this cycle was affected by dyneco                                      | bool           |
| Dump time                             | Dump time, if beam was dumped                                             | float          |
| Effective Spill Length                | Could also use duty factor (% of max possible spill length)               | float          |
| Operational cycle                     | True: operational, false: something like an MD                            | bool           |
| Time since B last trim                |                                                                           |                |
| SC number                             |                                                                           |                |
| Time since last upstream cycle change |                                                                           |                |
|                                       |                                                                           |                |
