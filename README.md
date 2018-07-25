Repository of Ansible Network Engine parsers.
Two type of parsers exists:
- cli: Parse from show commands to device facts containing current state.
- config: Parse from configuration to data easily consumable by Ansible modules and roles.

Examples
=========

config (`see in nxos/config/output/`): show_running-config_vlan.json
```
{
    "network_config.nxos_vlan": {
        "aggregate": [
            {
                "mapped_vni": null,
                "mode": null,
                "vlan_id": 2,
                "vlan_name": "vlan2",
                "vlan_state": null
            },
            {
                "mapped_vni": null,
                "mode": null,
                "vlan_id": 3,
                "vlan_name": "vlan3",
                "vlan_state": null
            }
        ]
    }
}
```

cli (`see in nxos/cli/output/`): show_vlan_brief.yaml
```
{
  "ansible_facts": {
    "network_facts": {
      "nxos": {
        "vlan": {
          "vlans": [
              {
                  "id": 1,
                  "name": "default",
                  "ports": [
                      "Ethernet1/3",
                      "Ethernet1/4",
                      "Ethernet1/6",
                      "Ethernet1/7",
                      "Ethernet1/8",
                      "Ethernet1/9",
                      "Ethernet1/10",
                      "Ethernet1/11",
                      "Ethernet1/12",
                      "Ethernet1/13",
                      "Ethernet1/14",
                      "Ethernet1/15",
                      "Ethernet1/16",
                      "Ethernet1/17",
                      "Ethernet1/18",
                      "Ethernet1/19",
                      "Ethernet1/20",
                      "Ethernet1/21",
                      "Ethernet1/22",
                      "Ethernet1/23",
                      "Ethernet1/24",
                      "Ethernet1/25",
                      "Ethernet1/26",
                      "Ethernet1/27",
                      "Ethernet1/28",
                      "Ethernet1/29",
                      "Ethernet1/30",
                      "Ethernet1/31",
                      "Ethernet1/32",
                      "Ethernet1/33",
                      "Ethernet1/34",
                      "Ethernet1/35",
                      "Ethernet1/36",
                      "Ethernet1/37",
                      "Ethernet1/38",
                      "Ethernet1/39",
                      "Ethernet1/40",
                      "Ethernet1/41",
                      "Ethernet1/42",
                      "Ethernet1/43",
                      "Ethernet1/44",
                      "Ethernet1/45",
                      "Ethernet1/46",
                      "Ethernet1/47",
                      "Ethernet1/48",
                      "Ethernet1/49",
                      "Ethernet1/50",
                      "Ethernet1/51",
                      "Ethernet1/52",
                      "Ethernet1/53",
                      "Ethernet1/54",
                      "Ethernet1/55",
                      "Ethernet1/56",
                      "Ethernet1/57",
                      "Ethernet1/58",
                      "Ethernet1/59",
                      "Ethernet1/60",
                      "Ethernet1/61",
                      "Ethernet1/62",
                      "Ethernet1/63",
                      "Ethernet1/64"
                  ],
                  "status": "active"
              },
              {
                  "id": 2,
                  "name": "vlan2",
                  "ports": null,
                  "status": "active"
              },
              {
                  "id": 3,
                  "name": "vlan3",
                  "ports": null,
                  "status": "act/lshut"
              }
          ]
        }
      }
    }
  }
}
```

CONTRIBUTING
=========

Folder structure is a 1:1 mapping between: parser:assert:input:output as per examples below:

```
<platform>/ <= Parser rules mapping parsed data to ansible modules.
├── show_running-config_vlan.yaml
└── show_vlan_brief.yaml

tests/<platform>/ <= Tests for every Parser rules.
├── assert <= Asserts to validate the parsed data
│   ├── show_running-config_vlan.yaml
│   └── show_vlan_brief.yaml
├── input <= Input data to parse
│   ├── show_running-config_vlan.txt
│   └── show_vlan_brief.txt
└── output <= Output containing the parsed data
    ├── show_running-config_vlan.json
    └── show_vlan_brief.json
```

Rules
------

For every parser:
- Filename: The command to parser the data, replacing `<space>` (space) by `<_>` (underscore).

- Data Structure Specification:
```
  network_facts: "Contains state data (!running-config)."
    <platform>: "Corresponding platform, equivalent to ansible_network_os."
      <command>:
        <subcommandN>:
          <attribute>: <value>
          <attribute>: <value>
          <attribute>: "Attributes with value/unit subkeys are useful when it is not clear if the value is K/kB/%/MB/G..."
              <value>: <value>
              <unit>: <value>
          <attributeS>: "Attributes ending with S are lists with rows."
            - <attribute>: <value>
              <attributeN>: <value>
            - <attribute>: <value>
              <attributeN>: <value>
            - <attribute>: <value>
              <attributeN>: <value>

  - network_config: "Contains configuration data (running-config)."
      <platform>: "Corresponding platform, equivalent to ansible_network_os."
        <module>: "Ansible Module name."
          aggregate: "Aggregation of entries supported by Ansible Module."
            - <module variable>: <value>
```

License
--------

GPLv3

Author
------

Victor da Costa (@victorock)
