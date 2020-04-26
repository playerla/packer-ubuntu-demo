# Packer ESX ubuntu demo

## Requirements

### Linux host

-   [OVF Tool](https://www.vmware.com/support/developer/ovf/)
-   [Packer](https://www.packer.io)

Remote ssh access and API access to ESX

### ESXi

```sh
# Allow ARP Packet Inspection of the Guest VM to infer the IP address
esxcli system settings advanced set -o /Net/GuestIPHack -i 1
# Enable inbound VNC 5900 to boot and configure iso (simulating keystroke). Can't add port to esx firewall so hack this rule.
esxcli network firewall ruleset set --enabled=true --ruleset-id=gdbserver
# Enable outbound Packer HTTP static server (preseed.cfg)
esxcli network firewall ruleset set --enabled=true --ruleset-id=httpClient
```

### Run

```sh
packer build ubuntu.json
```
