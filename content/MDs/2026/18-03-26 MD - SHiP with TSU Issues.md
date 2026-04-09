
Date: 2026-03-18
Logbook: https://logbook.cern.ch/elogbook-server/#/logbook?logbookId=424&dateFrom=2026-03-18T07%3A00%3A00&dateTo=2026-03-18T14%3A59%3A00

Cycles:

| Nickname | LSA name                                   | User    |
| -------- | ------------------------------------------ | ------- |
| ship     | MD_SHiP_L1230_East_Extraction_2026_MD18163 | SFTPRO2 |
| meas     | MD_14GeV_CHROMA_No_Ramp_2026_V1            | MD4     |
| md1      | MD_26_L1685_Q20_2026_V1                    | MD1     |

Three runs:

| Nickname | Description                 | Start          | End            |
| -------- | --------------------------- | -------------- | -------------- |
| Plain    | SHiP-Meas-MD1-MD1           | 10:20:10+01:00 | 11:50:00+01:00 |
| 1Z       | SHiP-ZERO-Meas-MD1-MD1      | 13:50:30+01:00 | 14:14:00+01:00 |
| 2Z       | SHiP-ZERO-ZERO-Meas-MD1-MD1 | 14:23:00+01:00 | 14:50:00+01:00 |

The plain SC didn't work (TSU red for beam injection on measurement cycle). This caused concern that Ship was causing injection problems with subsequent cycles, which would jeopordise Ship runs as a whole since the whole plan for Ship is to have many beam cycles in close series (e.g. ship-ship-ship-md1-sft). Beam would only be accepted for the 1Z and 2Z versions of the supercycle.

![[Pasted image 20260407160107.png]]

However, subsequent MDs performed by [Francesco and Nicolas (20th)](https://logbook.cern.ch/elogbook-server/#/logbook?logbookId=424&dateFrom=2026-03-20T06%3A30%3A01&dateTo=2026-03-20T12%3A30%3A01&eventToHighlight=4515468) and [Kevin and Tirsi (31st)](https://logbook.cern.ch/elogbook-server/#/logbook?logbookId=424&dateFrom=2026-03-31T15%3A00%3A00&dateTo=2026-03-31T22%3A59%3A00) confirmed that Ship is, in fact, fine. Rather, there is probably a timing issue with the measurement cycle (MD_14GeV_CHROMA_No_Ramp_2026_V1). We need to do a new MD to remedy this so it can actually be used.