# AgentActions Darwin Core Archive Extension

## Background & Warnings

This extension to Darwin Core under development is intended to permit sharing of attribution data for agents, which may be people or organizations.

### Features

1. Accommodates lists of agents as separate entries
2. Accommodates ordering for the lists of agents using an integer
3. Identifier types for agents are terms with definitions in a controlled vocabulary whose terms are externally referenced in VIVO
4. Optional roles for agents for individual entries in a controlled vocabulary of terms
5. A controlled vocabulary of terms for the types of identifiers for agents

### Shortcomings

1. Does not accommodate teams of agents
2. Does not accommodate reference to other extensions to Darwin Core such as identification histories

## Use in a local IPT

1. Install GBIF's Integrated Publishing Toolkit (IPT) in test mode. All requirements and install instructions can be found at [https://github.com/gbif/ipt/wiki/IPT2ManualNotes.wiki](https://github.com/gbif/ipt/wiki/IPT2ManualNotes.wiki).
2. Find ipt.properties in your IPT's data directory and add:

```
dev.registry.url=https\://tdwg.github.io/attribution/dwc
dev.registrydev.url=https\://tdwg.github.io/attribution/dwc
```

### Warning

The above hijacks the IPT into thinking GBIF's registry is somewhere else. You will receive a warning box something like:

```
IPT startup warnings. For additional help diagnosing the problem(s), please see logs. After fixing the problem(s), please restart your web server.
Couldn't load registered organisation 625a5522-1886-4998-be46-52c66dd566c9 from Registry: https://tdwg.github.io/attribution/dwc.
```

You can safely ignore these warnings.