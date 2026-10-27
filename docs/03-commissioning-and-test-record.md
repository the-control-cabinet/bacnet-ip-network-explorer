# 03 · Commissioning and Test Record

[← Back to README](../README.md)

**System:** BACnet/IP lab · **Device:** Room Controller simulator, instance 48, 192.168.0.112 · **Head-end:** Home Assistant OS VM (192.168.0.113) + Node-RED · **Date:** 1 July 2026

| # | Test | Method | Expected | Result | Pass |
|---|---|---|---|---|---|
| 1 | Device online | Start the simulator | Device ID and bound IP shown | Device Id 48, bound 192.168.0.112 | ✅ |
| 2 | Discovery (independent) | YABE BACnet/IP channel on UDP 47808 | I-Am from device 48 | `RoomController.Simulator [48]` at 192.168.0.112:50869 | ✅ |
| 3 | Object list | Expand the device in YABE | Object list retrieved | 13 objects (AI 0-2, AV 0-3, BV 0-1, MSV 0-1, CSV, Device) | ✅ |
| 4 | VM on the broadcast domain | HA VM bridged + promiscuous | VM has a LAN IP in the same /24 | `enp0s3` 192.168.0.113/24 | ✅ |
| 5 | ReadProperty AI 0 | Node-RED BACnet Read, Present_Value | Live temperature with units | 20.5 → 20.8 °C, objectType 0, instance 0 | ✅ |
| 6 | ReadProperty AV 0 | Node-RED BACnet Read, Present_Value | Setpoint matches the panel (T Set 21°) | 21 °C, objectType 2, instance 0 | ✅ |
| 7 | Repeat reads | Repeating inject | Fresh values each cycle | Logged 17:52:01 and 17:52:11, consistent | ✅ |
| 8 | Fault: NAT networking | VM NIC on NAT | No discovery | Nothing found → fixed by bridged + promiscuous | ✅ |
| 9 | Fault: wrong interface / broadcast | Wrong IP in the BACnet client | SERVICES error | Fixed with 192.168.0.113 / 192.168.0.255 | ✅ |

**Evidence:** tests 1-7 are visible in [images/project-2-screenshot.png](../images/project-2-screenshot.png), with close-ups in [images/](../images/). Tests 8-9 were met and resolved during the build and have no screenshot.

**Sign-off notes:** simulator only; read-only tests. No writes were made.
