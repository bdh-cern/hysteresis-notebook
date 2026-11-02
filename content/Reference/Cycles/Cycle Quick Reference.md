
| User              | Momentum Peak  / GeV/c | FT Length / s |
| ----------------- | ---------------------- | ------------- |
| SFTION1           | 380                    | 9             |
| SFTPRO1           | 400                    | 5             |
| AWAKE             | 400                    | 0.9           |
| SHiP              | 400                    | 1.2           |
| HIRADMAT          | 440                    | 2             |
| LHC, INDIV, PILOT | 450                    | 0.5           |
| LHCION            | 450                    | 1.2 + 1       |

# Quick Info Format

This is a schema for quick info, for Claude etc. to populate with important facts about certain cycles. This should be re-ingested everytime a factsheet is requested.

| Field                         | Value                                                                             |
| ----------------------------- | --------------------------------------------------------------------------------- |
| Representative cycle name     | (The name of the specific cycle for which the following variables were retrieved) |
| User                          | (The LSA user)                                                                    |
| Total length (ms)             | (The total length in ms)                                                          |
| Total length (BPs)            | (The total length in BPs)                                                         |
| Time of first injection       | (The cycle-time at which the first injection occurs)                              |
| Times of other injections     | (Array of cycle-times for any other injections)                                   |
| \[Category\] range            | (e.g. '0 - 200 ms (200ms; 0.17BPs)')                                              |
| Debunching time               | (The cycle time at which debunching happens)                                      |
| Max dipole field              | (The highest field of the cycle)                                                  |
| Max momentum                  | (The highest momentum of the cycle)                                               |
| Max dipole current            | (The highest dipole current of the cycle)                                         |
| Max quadrupole current        | (The highest quadrupole current of the cycle)                                     |
| Injected intensity            | (The typical injected intensity, rounded)                                         |
| Injection plateau momentum    | (The momentum of the beam at injection)                                           |
| Crosses transition            | (True/false)                                                                      |

For Claude: when compiling a factsheet about a cycle, populate the above table, create a plot of the cycle with intensity and field shown, and add vertical dashed lines to deliniate the beam processes.

At the bottom of the factsheet, add 'Cycle Names' and a list of all relevant cycle names for the cycle archetype.

Further preferences:
- Use only LSA (pjlsa) and NXCALS data; do not draw on other notebook pages.
- Value brevity: give only the quantity asked, no extras, no sources.
- Write 'none' as -/-; give ranges as 'A - B \[unit\]'.
- Spaces between numbers and their units.
- Use exponent format (xE+-Y) where appropriate
- Name beam-process rows by category (Pre-injection, Injection plateau, Ramp, Flat-top, Ramp-down), not by LSA name.
- Add a 'Beam Process Names' section, listing every beam process of the cycle, above 'Cycle Names'.
- Draw the beam-process lines in a subtle grey.
- No markers on the plot lines.