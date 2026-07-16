- Why do the NMR measurements appear to drift
- What are the three bands on the plot
- More conclusions to MD part 1

****
# Testing Device

- First test:

```

  "configuration" : {
  "trim_context" : "SPS.USER.SFTPRO3",
  "max_bhys_change" : 2.0E-4,
  "min_bhys_change" : 5.0E-6,
  "max_corrected_b" : 1.8025,
  "min_corrected_b" : 1.8,
  "flattop_reference_cycletime_ms" : 7000,
  "start_of_correction_cycletime_ms" : 5000,
  "correction_factor" : 0.6,
  "working_point_b" : 1.81455,
  "drive" : true,
  "send_trim" : true,
  "correctable_supercycle_compositions" : [ [ "SFTPRO3", "MD1", "SFTPRO3", "MD1", "SFTPRO3", "MD1" ] ]
}
```

![[Pasted image 20260623125352.png]]

- Second test:

Since the correction overshot and slowly recovered, I decreased the max_bhys_change (to damp the overshoot) and increased the correction factor (to make the change faster when correction_factor x delta < max... i.e. on the recovery )

```

  "configuration" : {
  "trim_context" : "SPS.USER.SFTPRO3",
  "max_bhys_change" : 1.0E-4,
  "min_bhys_change" : 5.0E-6,
  "max_corrected_b" : 1.8025,
  "min_corrected_b" : 1.8,
  "flattop_reference_cycletime_ms" : 7000,
  "start_of_correction_cycletime_ms" : 5000,
  "correction_factor" : 0.8,
  "working_point_b" : 1.81455,
  "drive" : true,
  "send_trim" : true,
  "correctable_supercycle_compositions" : [ [ "SFTPRO3", "MD1", "SFTPRO3", "MD1", "SFTPRO3", "MD1" ] ]
}
```

- 