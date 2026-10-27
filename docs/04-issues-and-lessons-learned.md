# 04 · Issues and Lessons Learned

[← Back to README](../README.md)

Each issue is written up as symptom → cause → fix → lesson.

### 1. Who-Is from the VM found nothing
- **Symptom:** YABE on the host could see device 48, but nothing inside the HA VM could.
- **Cause:** the VirtualBox NIC was on NAT and/or promiscuous mode was off, so the subnet's UDP broadcasts never reached the VM.
- **Fix:** **Bridged Adapter** + **Promiscuous Mode: Allow All**. The VM then took its own LAN address (192.168.0.113).
- **Lesson:** BACnet/IP discovery is broadcast-based, so anything that splits the broadcast domain breaks it. That includes NAT, VLANs and routers without a BBMD.

### 2. SERVICES error from the Node-RED BACnet nodes
- **Symptom:** the BACnet nodes failed to start their services.
- **Cause:** the client's interface IP and broadcast address didn't match the VM's real network.
- **Fix:** interface = **192.168.0.113** (the VM), broadcast = **192.168.0.255**.
- **Lesson:** a BACnet client must bind to the right NIC. Multi-homed hosts (VMs, laptops on Wi-Fi plus Ethernet) are the usual trap.

### 3. Treating BACnet like registers
- **Symptom:** wrong or empty reads.
- **Cause:** thinking in "address numbers" instead of object type + instance + property.
- **Fix:** read **Analog Input 0 / Present_Value (85)** and **Analog Value 0 / Present_Value (85)** explicitly.
- **Lesson:** BACnet's richer model needs more precise addressing, but in return it gives you names and units.

### 4. Most of the time went on networking
- About five hours to the first successful read. The majority went on VM networking, not on BACnet or Node-RED configuration.

### Observation: the device listed twice
YABE showed `RoomController.Simulator [48]` twice under the same UDP channel. That usually means the device's I-Am was received twice, for example after more than one Who-Is, or via more than one route. It didn't affect the reads. On a real site, duplicate device instances are a genuine fault, because every device instance on a BACnet internetwork must be unique, so it's worth knowing what a duplicate looks like.

## Transferable field lessons

- BACnet/IP faults are usually Layer 2/3 (broadcasts, NAT, VLANs, firewalls, BBMDs) before they are BACnet.
- Verify with an independent explorer (YABE) before blaming the head-end.
- Record each device's instance, IP and port in the handover. Device instance uniqueness matters.
