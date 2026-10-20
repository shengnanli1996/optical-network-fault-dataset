# Data collection

## Experimental systems

The dataset was collected from three independent laboratory configurations built with commercial optical transport equipment:

1. a point-to-point optical multiplex section protection system with two 40 km routes;
2. a modified point-to-point protected system with different fiber and VOA placements; and
3. a six-node network containing 14 network elements across two equipment platforms.

Logical topologies, rack layouts, board-level functional diagrams, and port-level connection tables are included in this repository.

## Data sources

Each snapshot combines three sources from the network management system:

- **PM:** real-time performance values collected through a REST interface. Requests were batched with no more than 10 managed resources per request. Returned records were regrouped by network element before saving.
- **Alarms:** the complete set of active, uncleared alarms collected through a REST interface.
- **OCM:** XML responses collected through an optical-channel monitoring interface. Ports on the same OPM8 board were queried sequentially with a 0.3 s request interval, while different boards in the six-node topology were queried concurrently.

An OCM request can return HTTP 500 with a `Query data but return empty` reason when no optical signal is observable. These responses are valid experimental observations and are retained. Their status is recorded in `manifest.csv`.

## Fault emulation

### Single-fiber cuts

One physical connection was disconnected for each case. A snapshot was collected before the disconnection and another after it. Topology 1 repeated each location three times; topologies 2 and 3 used one run per location.

### Dual-fiber cuts

Six selected connections in topology 3 were used to create 30 ordered two-fault experiments. Each experiment contains three states: before either cut, after the first cut, and after the second cut while the first cut remained present.

### Progressive degradation

VOA channels had a 2 dB baseline setting. For each selected VOA, data were collected at the baseline and after each 0.5 dB increase up to an absolute setting of 20 dB. The filename and manifest report the additional attenuation relative to the 2 dB baseline, from 0 to 18 dB. The script waited 10 s after each VOA adjustment before collecting the next snapshot. After the sweep, the VOA was returned to 2 dB and one reset snapshot was collected.

### Board failures

Board failures were emulated by removing one board at a time in topology 3. The pre-fault snapshot includes all configured PM resources. The post-fault PM query excludes ports belonging to the removed board because those resources are unavailable. Alarm and OCM collection otherwise follows the same procedure.

## Snapshot definition

A snapshot is one multi-source acquisition at a specified topology, experiment case, and network state. It includes one alarm file, one PM file per queried network element, and one OCM XML file per queried monitoring port. The exact file membership of every snapshot is listed in `metadata/manifest.csv`.

