# File naming and labels

## Single-fiber cuts

Examples:

```text
C001_R1_before_fiber_cut_PM_NE1-1.json
C001_R1_after_fiber_cut_Alarm.json
C001_after_fiber_cut_OPM_NE1-1_PORT1.xml
```

`C001` identifies the disconnected connection in `fiber_cut_cases.csv`. `R1`, `R2`, and `R3` are repeated runs used only in topology 1. `before` and `after` indicate the network state relative to the fiber disconnection.

## Dual-fiber cuts

Examples:

```text
C009_C031_before_dual_fiber_cut_Alarm.json
C009_C031_after_C009_dual_fiber_cut_PM_NE1-1.json
C009_C031_after_C009_C031_dual_fiber_cut_OPM_NE1-1_PORT1.xml
```

The first two identifiers define an ordered experiment. The three states mean:

1. neither connection is cut;
2. the first connection is cut; and
3. both connections are cut.

The 30 ordered combinations are listed in `dual_fiber_cut_cases.csv`.

## Board failures

Examples:

```text
B001_before_board_failure_Alarm.json
B001_after_board_failure_PM_NE1-1.json
```

`B001` maps to a network element, slot, and board type in `board_failure_cases.csv`.

## Progressive degradation

Examples:

```text
VOA_0dB_PM_NE1-1.json
VOA_0.5dB_Alarm.json
VOA_18dB_OPM_NE1-1_PORT1.xml
VOA_reset_Alarm.json
```

The attenuation in a filename is additional attenuation relative to the 2 dB VOA baseline. The directory and `voa_index` manifest column identify the physical VOA location. `VOA_reset` is collected after restoring the attenuator to 2 dB.

## Data suffixes

- `_Alarm.json`: active alarms for the snapshot.
- `_PM_<network-element>.json`: real-time PM resources grouped by network element.
- `_OPM_<network-element>_PORT<port>.xml` or `_OPM_PORT<port>.xml`: channel-power response from one OPM8 monitoring-board input. The `OPM` filename token is retained for provenance; public documentation uses OCM.

