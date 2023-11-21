---
title: "Data Properties"
date: 2023-05-18T13:31:46+0000
weight: 20
---

To support a VSS data model Ford has defined a profile with extended attributes as well as a totally new node type.

## Definition

The following extended attributes are added.

For branches:

```yaml
<VSS Branch name>:
  type: branch
  description: ...
  identifier: <identifier>
  elementType: [FeatureOfInterest|Node]
  definition: ...
```

For sensor/attribute/actuators:

```yaml
<VSS Signal name>:
  type: <VSS type>
  description: ...
  identifier: <identifier>
  elementType: SignalType
  definition: ...
  property: ...
```

In addition to this a new node type `dataProperty` is added.

```yaml
<VSS Data Property Name>:
  type: dataProperty
  description: ...
  identifier: <identifier>
  elementType: [DataProperty | ObjectProperty]
  definition: ...
```

It is for now assumed that `dataProperty` nodes must exist in the types tree, similar to how structs are managed.

## Tool Support

The extended attributes for branches and signals are supported for vss-tools JSON/Yaml.

The new node type `dataProperty` is currently not supported.
VSS-tools could possibly add support for new node types, but performing semantic checks would be more difficult.


## Usage

TBD


## References
