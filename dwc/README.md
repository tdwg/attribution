# AgentActions Darwin Core Archive Extension

1. Install GBIF's Integrated Publishing Toolkit (IPT) in test mode. All requirements and install instructions can be found at [https://github.com/gbif/ipt/wiki/IPT2ManualNotes.wiki](https://github.com/gbif/ipt/wiki/IPT2ManualNotes.wiki).
2. Find ipt.properties in your IPT's data directory and add:

```
dev.registry.url=https\://tdwg.github.io/attribution/dwc
dev.registrydev.url=https\://tdwg.github.io/attribution/dwc
```

## Warning

The above hijacks the IPT into thinking GBIF's registry is somewhere else. You will receive a warning box something like:

```
IPT startup warnings. For additional help diagnosing the problem(s), please see logs. After fixing the problem(s), please restart your web server.
Couldn't load registered organisation 625a5522-1886-4998-be46-52c66dd566c9 from Registry: https://tdwg.github.io/attribution/dwc.
```

You can safely ignore these warnings.