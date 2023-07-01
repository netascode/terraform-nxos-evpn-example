# Cisco Nexus 9000 EVPN Terraform Example

This example demonstrates how the [NX-OS Terraform Provider](https://registry.terraform.io/providers/CiscoDevNet/nxos/latest/docs) can be used to build a Cisco Nexus 9000 EVPN Fabric. It currently supports underlay and overlay configuration, but no access interfaces.

It uses the following Terraform Modules:

- [EVPN OSPF Underlay Module](https://registry.terraform.io/modules/netascode/evpn-ospf-underlay/nxos/latest)
- [EVPN Overlay Module](https://registry.terraform.io/modules/netascode/evpn-overlay/nxos/latest)

The configuration is derived from a set of yaml files in the `data` [directory](https://github.com/netascode/terraform-nxos-evpn-example/tree/main/data).

To point this to your own Nexus 9000 fabric, update the `data/inventory.yaml` file accordingly.

```yaml
---
fabric:
  inventory:
    spines:
      - name: SPINE-1
        url: https://10.1.1.1
      - name: SPINE-2
        url: https://10.1.1.2

    leafs:
      - name: LEAF-1
        url: https://10.1.1.3
      - name: LEAF-2
        url: https://10.1.1.4
```

Credentials can either be provided via environment variables:

```shell
export NXOS_USERNAME=admin
export NXOS_PASSWORD=Cisco123
```

Or by updating the provider configuration in `main.tf`:

```terraform
provider "nxos" {
  username = admin
  password = Cisco123
  devices  = local.devices
}
```
