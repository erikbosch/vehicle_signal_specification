---
title: "DBC Mapping"
date: 2023-05-18T13:31:46+0000
weight: 10
---

For mapping between VSS signals and CAN signals defined in DBC files the Eclipse KUKSA project has defined two extended attributes,
`vss2dbc` and `dbc2vss`


## Definition

The profile defines two extended attributes, one for each direction of mapping

* `vss2dbc` for mapping from VSS signal to CAN signal
* `dbc2vss` for mapping from CAN signal to VSS signal

For both of them it is possible to specify how values shall be converted, by a mapping table or by a mathematical formula.
For mapping from CAN to VSS it is possibly to specify how often the VSS signal shall be updated.

```yaml
<VSS Signal name>:
  type: <VSS type>
  datatype: <VSS datatype>
  vss2dbc:
    signal: <DBC signal name>
    [transform: ...]
  dbc2vss:
    signal: <DBC signal name>
    [interval_ms: <interval in milliseconds>]
    [on_change: {true|false}]
    [transform: ...]
```

Example:


```yaml
Vehicle.Body.Mirrors.DriverSide.Tilt:
  datatype: int8
  type: actuator
  dbc2vss:
    signal: VCLEFT_mirrorTiltYPosition
    interval_ms: 100
    transform:
      math: "floor((x*40)-100)"
  vss2dbc:
    signal: VCLEFT_mirrorTiltYPosition
    transform:
      math: "(x+100)/40"
```

For more information on syntax see [KUKSA Documentation](https://github.com/eclipse/kuksa.val.feeders/edit/main/dbc2val/mapping/mapping.md)

## Tool Support

If you use `-e vss2dbc,dbc2vss` in vss-tools then JSON and Yaml output will contain the mapping.
The overlay mechanism can be used to add the profile.


## Usage

Below is an example using an overlay to specify vss2dbc/dbc2vss extensions

```
vss-tools/vspec2json.py -e vss2dbc,dbc2vss -o dbc_overlay.vspec -u spec/units.yaml  --json-pretty ./spec/VehicleSignalSpecification.vspec vss_dbc.json
```


## References
