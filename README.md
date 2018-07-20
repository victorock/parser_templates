Repository of Ansible Network Engine parsers.
Two type of parsers exists:
- cli: Parse from show commands to device facts containing current state.
- config: Parse from configuration to data easily consumable by Ansible modules and roles.

Examples
=========

config (`see in nxos/config/output/`): nxos_vlan.json
```
{
  "ansible_facts": {
    "network_config": {
      "nxos_vlan": [
        {
            "mapped_vni": 0,
            "mode": "ce",
            "name": "vlan2",
            "vlan_id": 2,
            "vlan_state": "active"
        },
        {
            "mapped_vni": 0,
            "mode": "ce",
            "name": "vlan3",
            "vlan_id": 3,
            "vlan_state": "active"
        }
      ]
    }
  }
}
```

cli (`see in nxos/cli/output/`): show_vlan_brief.yaml
```
{
  "ansible_facts": {
    "network_facts": {
      "nxos_vlan": {
          "1": {
            "name": "default",
            "ports": [
                "Eth1/3",
                "Eth1/4",
                "Eth1/6",
                "Eth1/7",
                "Eth1/8",
                "Eth1/9",
                "Eth1/10",
                "Eth1/11",
                "Eth1/12",
                "Eth1/13",
                "Eth1/14",
                "Eth1/15",
                "Eth1/16",
                "Eth1/17",
                "Eth1/18",
                "Eth1/19",
                "Eth1/20",
                "Eth1/21",
                "Eth1/22",
                "Eth1/23",
                "Eth1/24",
                "Eth1/25",
                "Eth1/26",
                "Eth1/27",
                "Eth1/28",
                "Eth1/29",
                "Eth1/30",
                "Eth1/31",
                "Eth1/32",
                "Eth1/33",
                "Eth1/34",
                "Eth1/35",
                "Eth1/36",
                "Eth1/37",
                "Eth1/38",
                "Eth1/39",
                "Eth1/40",
                "Eth1/41",
                "Eth1/42",
                "Eth1/43",
                "Eth1/44",
                "Eth1/45",
                "Eth1/46",
                "Eth1/47",
                "Eth1/48",
                "Eth1/49",
                "Eth1/50",
                "Eth1/51",
                "Eth1/52",
                "Eth1/53",
                "Eth1/54",
                "Eth1/55",
                "Eth1/56",
                "Eth1/57",
                "Eth1/58",
                "Eth1/59",
                "Eth1/60",
                "Eth1/61",
                "Eth1/62",
                "Eth1/63",
                "Eth1/64"
            ],
            "status": "active"
        },
        "2": {
            "name": "vlan2",
            "ports": null,
            "status": "active"
        },
        "3": {
            "name": "vlan3",
            "ports": null,
            "status": "act/lshut"
        }
      }
    }
  }
}
```

CONTRIBUTING
=========

Folder structure:
```
<platform>/
├── cli
│   ├── assert <= Asserts to validate the parsed data
│   │   └── <show_command_with_underscores>.yaml
│   ├── fact <= Parser rules for each command to parse
│   │   └── <show_command_with_underscores>.yaml
│   ├── input <= Input data to parse
│   |    └── <show_command_with_underscores>.txt
│   └── output <= Output containing the parsed data
│       └── <show_command_with_underscores>.json
└── config
    ├── assert <= Asserts to validate the parsed data
    │   └── <ansible_module_or_role_name>.yaml
    ├── module <= Parser rules mapping parsed data to ansible modules
    │   └── <ansible_module_or_role_name>.yaml
    └── input <= Input data to parse
    │   └── <ansible_module_or_role_name>.txt
    └── output <= Output containing the parsed data
        └── <show_command_with_underscores>.json
```


License
------------

GPLv3

Author
------------

Victor da Costa (@victorock)
