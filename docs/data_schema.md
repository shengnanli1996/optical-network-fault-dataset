# Data schema

## Manifest

`metadata/manifest.csv` contains one row per released data file.

| Column | Meaning |
|---|---|
| `topology` | Independent experimental environment: `topology_1`, `topology_2`, or `topology_3` |
| `data_type` | `alarm`, `pm`, or `ocm` |
| `snapshot_prefix` | Common filename prefix for files collected in one experimental state |
| `fault_type` | `fiber_cut`, `dual_fiber_cut`, `fiber_degradation`, or `board_failure` |
| `case_id` | Fiber-cut case identifier or combined ordered case label |
| `board_id` | Board-failure identifier, if applicable |
| `state` | `before`, `after`, a dual-cut state, `degraded`, or `reset` |
| `voa_index` | VOA number within its topology |
| `attenuation_db` | Added attenuation relative to the 2 dB baseline |
| `node` | Network element associated with a PM or OCM file |
| `ocm_port` | OCM input-port number associated with an XML file |
| `record_count` | Number of PM resources, alarm records, or channel-power records in the file |
| `result_status` | OCM result: `channel_power_returned` or `empty_channel_power` |
| `relative_path` | File location inside the public data archive |
| `source_relative_path` | Provenance path within the internal collection directory; it contains no absolute local path |
| `sha256` | SHA-256 digest of the released file |

For VOA experiments, `snapshot_prefix` repeats across different VOA indices. A unique snapshot key is therefore the combination of `topology`, `snapshot_prefix`, and `voa_index`.

## Alarm JSON

The original alarm object hierarchy is retained. Public processing:

- replaces the management-domain name with `NMS`;
- maps product types to `platform_A` or `platform_B` in individual records;
- removes resource URLs and management IP addresses;
- translates alarm names, probable causes, locations, and additional information to English; and
- replaces internal UUIDs with stable, topology-scoped anonymous identifiers.

Native alarm codes and reason identifiers are retained. Alarm names and probable causes are summarized in `metadata/alarm_dictionary.csv`.

## PM JSON

The vendor-prefixed top-level output key is renamed to `pm-output`. Each resource contains its network element, resource name and type, timestamped PM values, indicator identifiers, and units. Internal UUIDs are replaced with topology-scoped identifiers. Chinese location text and units are translated or normalized.

The observed PM indicators and their units are described in `metadata/pm_metric_dictionary.csv`.

## OCM XML

The SOAP/TM Forum XML hierarchy returned by the interface is retained so that channel frequency or wavelength and optical power remain traceable to the source response. Credential-bearing security elements and request-specific operation UUIDs are removed.

An XML file can contain either channel-power records or the original empty-data response. Both are valid. Use `record_count` and `result_status` in the manifest to distinguish them.

Although filenames contain `OPM` because the physical boards are named OPM8, the released measurements are documented as OCM channel-power data rather than continuous spectra.

## Identifier scope

Each topology has its own anonymous identifier namespace. The same source resource maps consistently between alarm and PM data inside one topology. No cross-topology identity is implied, and raw UUID mappings are not released.

