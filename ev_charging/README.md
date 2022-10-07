# Proposal on how to use GitHub for EV Charging project

## Long term vision

Vehicle related signals integrated into [VSS](https://github.com/COVESA/vehicle_signal_specification).
Infrastructure-related signals stored in a new repo in COVESA, not in VSS.

## Short term working model

The project shall use a fork of VSS for ongoing development.
This could be a "company fork" or a "personal fork", the important part is that someone active in EV Charging project has maintainer rights 
to that fork and can push changes, approve pull requests and add additional contributors (i.e. others that can write to the fork).
When project has reached a stable state a pull request to official VSS repo can be created.

During development infrastructure-related signals can reside in the fork.
They shall however be removed before a pull request to official VSS is created.

## General work flow

Signals can be added/changed by direct push by project/fork maintainers.
Others need to create pull requests.

For linking to EV Charging project excel as custom attribute `evc` could be used to specify the identifier used in project documentation outside Github.
This can also be added to existing signals as an intermediate solution to simplify search, but they shall be removed before merging to official VSS.
A custom attribute `evc_comment` can be used to cover to discussion topics.

Example:

```
TimeZone:
  type: attribute
  datatype: float
  min: -12
  max: 12
  evc: time_zone
  description: Current offset at the location of the charging station.
  evc_comment: There is no standard for designations like CET, PST, so they might be ambiguous.
               Value might vary over the year due to DST policy.
```

## Workflow for VSS signals

### Reusing or Changing existing signals

If a reasonable signal already exist it can possibly be reused also for the EV Charging project.
If no change is needed just add the `evc` attribute to specify which EV project data it corresponds to.
If changes are needed (and likely will be accepted by VSS project) do the change. Possibly use `evc_comment`to give a rationale.
Any changes will need to be discussed/agreed with VSS project before being merged to standard VSS.
Changes affecting backward compatibility shall if possible be minimized.

### Adding new signals

To get best overview they shall be added at a logical place in the VSS Tree, matching already existing signals.

## Workflow for Infrastructure signals

Two files have been created; [Infrastructure.md](Infrastructure.md) and [ChargingStation.md](ChargingStation.md). If needed additional files can be added under ChargingStation.md.


## Building

Clone VSS and make sure submodules are fetched

```bash
cd vehicle_signal_specification
git submodule update --init
```

Follow [vss-tools](https://github.com/COVESA/vss-tools) instructions to install the Python development environment.

To build VSS signals and generate excel:

```bash
user@debian:~/vehicle_signal_specification$ ./vss-tools/vspec2csv.py -e evc,evc_comment ./spec/VehicleSignalSpecification.vspec ev_vss.csv
Output to csv format
Known extended attributes: evc, evc_comment
Loading vspec from ./spec/VehicleSignalSpecification.vspec...
Calling exporter...
Generating CSV output...
All done.
```
To build infrastructure signals:

```bash
user@debian:~/vehicle_signal_specification$ ./vss-tools/vspec2csv.py -e evc,evc_comment ./ev_charging/Infrastructure.vspec ev_infrastructure.csv
Output to csv format
Known extended attributes: evc, evc_comment
Loading vspec from ./ev_charging/Infrastructure.vspec...
Calling exporter...
Generating CSV output...
All done.
```

Other output formats exist, see [VSS-tools](https://github.com/COVESA/vss-tools)


