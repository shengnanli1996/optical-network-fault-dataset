# An Open Multi-Topology and Multi-Source Dataset for Alarm Analysis and Fault Diagnosis in Optical Networks

This repository documents an experimental optical transport network fault dataset collected from commercial optical transport equipment and its network management system. The dataset covers two point-to-point optical multiplex section protection configurations and one six-node network. Each data snapshot combines active alarms, real-time performance monitoring (PM) measurements, and optical channel monitor (OCM) channel-power measurements.

![Experimental topologies and data acquisition](figures/dataset_overview.png)

## Dataset at a glance

| Topology | Configuration | Fault scenarios | Snapshots |
|---|---|---|---:|
| `topology_1` | Point-to-point protected system, configuration 1 | 37 single-fiber cuts with three repetitions; degradation at 5 VOA locations | 412 |
| `topology_2` | Point-to-point protected system, configuration 2 | 40 single-fiber cuts; degradation at 6 VOA locations | 308 |
| `topology_3` | Six-node network with 14 network elements | 220 single-fiber cuts; 30 ordered dual-fiber-cut experiments; degradation at 8 VOA locations; 58 board failures | 950 |
| **Total** | 3 experimental topologies | 4 fault categories | **1,670** |

The complete release contains **45,429 data files**:

- **16,179 PM JSON files**, containing 129,363 port-level PM records and 670,947 metric values;
- **1,670 alarm JSON files**, containing 6,361 active-alarm records;
- **27,580 OCM XML files**, containing 296,343 channel-power records.

## Download

The complete data are distributed as three topology-specific archives through the repository's [Releases page](https://github.com/shengnanli1996/optical-network-fault-dataset/releases). The release also provides SHA-256 checksums. Repository files contain the metadata, data dictionaries, diagrams, and representative examples required to interpret the archives.

## Repository contents

```text
.
├── docs/                     Dataset structure, collection, naming, and use notes
├── figures/                  Logical topologies, rack layouts, and board diagrams
├── metadata/
│   ├── manifest.csv          One row per data file, including SHA-256
│   ├── alarm_dictionary.csv  English alarm descriptions and probable causes
│   ├── pm_metric_dictionary.csv
│   ├── connection_tables/    Port-level physical connections for each topology
│   └── fault_labels/         Fiber-cut, VOA, board-failure, and OCM locations
└── samples/                  One representative alarm, PM, and OCM file
```

Detailed documentation:

- [Data collection](docs/data_collection.md)
- [Data schema](docs/data_schema.md)
- [File naming and labels](docs/file_naming.md)
- [Responsible use](docs/responsible_use.md)

## Fault labels and physical locations

The dataset uses explicit physical identifiers:

- `Cxxx` identifies one row in a topology's connection table. For a single-fiber-cut experiment, it is the disconnected fiber connection.
- Ordered dual-fiber-cut experiments identify the first and second disconnected connections separately.
- `Bxxx` identifies a network element, slot, and board in `board_failure_cases.csv`.
- `VOAx` identifies an attenuator channel in `voa_locations.csv`.

The three topologies are independent experimental environments. Anonymous resource identifiers are stable only within one topology and must not be joined across topologies.

## OCM terminology

The installed monitoring boards are named OPM8 by the equipment vendor, and the original XML filenames therefore contain `OPM`. The retained measurements are per-channel optical powers rather than continuous optical spectra. This repository consequently uses **optical channel monitor (OCM)** and **channel-power records** in its documentation and metadata. Original XML filenames are preserved for provenance.

## Anonymization and processing

Public files are English and vendor-neutral at the record level. Internal resource UUIDs are replaced with topology-scoped anonymous identifiers. Management addresses, resource URLs, credentials, XML security elements, and operation UUIDs are removed. Exact equipment provenance is retained separately in `metadata/hardware_metadata.json`.

The transformation report records file counts and residual scans for Chinese text, vendor-specific terms, UUIDs, IPv4 addresses, and XML credential fields. Raw-to-anonymous identifier mappings are intentionally excluded from this repository.

## Examples

The `samples/` directory contains one representative post-fault snapshot from `topology_3`. JSON, XML, and CSV are standard formats and do not require custom loading software.

## Licence and citation

Except where otherwise noted, the dataset, metadata, documentation, and figures in this repository are licensed under the [Creative Commons Attribution 4.0 International License](LICENSE) (CC BY 4.0). This licence permits sharing and adaptation, including commercial use, provided that appropriate credit is given, the licence is linked, and changes are indicated. Product names and trademarks are used only for factual identification and are not licensed by this repository.

Current dataset authors:

- Shengnan Li
- Fubin Wang
- Min Zhang
- Danshi Wang (corresponding author, `danshi_wang@bupt.edu.cn`)

All authors are affiliated with the State Key Laboratory of Information Photonics and Optical Communications, Beijing University of Posts and Telecommunications (BUPT). Citation metadata are provided in [`CITATION.cff`](CITATION.cff).
