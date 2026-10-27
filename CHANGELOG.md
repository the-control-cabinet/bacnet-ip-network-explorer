# Changelog

## [1.1.0] - 2026-10-26
### Changed
- Documentation rebuilt from the captured evidence:
  - full 13-object list recorded
  - Set Point corrected to **Analog Value 0** (was listed as AV 1)
  - simulator bound address (192.168.0.112:50869), VM address (192.168.0.113) and HA Core version recorded
  - flow structure (repeating inject → 2 × BACnet Read → functions → debug) documented
### Added
- Points list, commissioning and test record, Who-Is/ReadProperty sequence diagram, BACnet vs Modbus comparison from both projects, duplicate-device observation, evidence close-ups, video section, portfolio links.
### Note
- `config/flows.json` is a placeholder until the real Node-RED export is added (see `config/README.md`).

## [1.0.0] - 2026-07-01
### Added
- Node-RED BACnet Read flow for AI 0 (Indoor Temperature) and AV 0 (Set Point).
- YABE Room Controller simulator (device 48) discovery.
- Home Assistant OS in VirtualBox with bridged + promiscuous networking.
### Fixed
- Device discovery from the VM, SERVICES errors (interface and broadcast), object/property addressing.
