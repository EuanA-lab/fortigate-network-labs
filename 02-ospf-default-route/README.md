fortigate-network-labs/
├── README.md
├── Lab-1-image.png
└── 02-ospf-default-route/
    └── README.md
# Lab 02 - OSPF Default Route & Internet Breakout

## Purpose

The purpose of this lab is to build on the OSPF network created in Lab 01 by configuring FW01 as the central Internet edge firewall.

FW02 will have its direct Internet connection removed and will instead learn a default route dynamically from FW01 using OSPF. Traffic from the FW02 LAN will then use FW01 for Internet access.

This lab will demonstrate how a default route can be originated into OSPF and how routing, firewall policies and NAT work together to provide Internet access through a central edge firewall.

## Starting State

Lab 02 begins with the working OSPF topology from Lab 01. Both FortiGates currently have direct Internet connectivity through their `port1` interfaces.

Before making any changes, the routing table on FW02 was recorded to provide a baseline.

### FW02 Routing Table

<img width="672" height="133" alt="image" src="https://github.com/user-attachments/assets/1fa9a048-b002-4e09-a07a-1466879ae34d" />

Port1 status set to down, default route removed from routing table

<img width="710" height="101" alt="image" src="https://github.com/user-attachments/assets/8ca1b8aa-987c-4dcb-a0fc-50b71f465dc5" />

### FW01 Routing Table

<img width="637" height="150" alt="image" src="https://github.com/user-attachments/assets/934cf766-830f-431c-8115-fb11dfbff55b" />

### Configuration

On FW01 we run the commands 

config router ospf
    set default-information-originate enable
end

Once done we verify FW02 routing table

<img width="636" height="84" alt="image" src="https://github.com/user-attachments/assets/81307e63-1ea5-4604-b99e-2427e87bcfb8" />

### Troubleshooting

Although FW02 successfully learned the default route through OSPF, Internet-bound traffic was initially unable to traverse FW01.

On FW01 we required an additional firewall policy to allow traffic from port 2 to traverse out port 1, with NAT enabled

<img width="545" height="257" alt="image" src="https://github.com/user-attachments/assets/fff1c212-2096-47e7-9c7f-5abbafb5fb80" />

Verified connectivity from PC02

<img width="548" height="250" alt="image" src="https://github.com/user-attachments/assets/c659801d-f56d-4652-90de-37d71dbba12b" />

