# Representative files

These three files come from the same post-fault snapshot: the `C001` single-fiber cut in `topology_3`.

- `alarm_example.json`: all active alarms returned for the snapshot.
- `pm_example.json`: real-time PM records for network element `NE1-1`.
- `ocm_example.xml`: the OCM channel-power response for `NE1-1`, monitoring port 1.

The complete snapshot contains additional PM and OCM files. Its complete membership can be found by filtering `metadata/manifest.csv` for:

```text
topology = topology_3
snapshot_prefix = C001_after_fiber_cut
```

