# EasyEDA USB-C Power Supply

This repository contains a simple USB-C power-supply design scaffold inspired by RobertFeranec's video, "How to design a USB-C Power Supply (5V to 28V) in 3 hours".

The project is named EasyEDA-USB-C-Power-Supply and is intended to provide a practical reference for building a USB-C PD-based 5V to 28V source.

The purpose of this project is to provide a clean starting point for a USB-C PD based bench or lab supply that can negotiate and regulate a 5 V to 28 V output range.

## Design goals

- USB-C input and Power Delivery negotiation
- Adjustable output from 5 V to 28 V
- Suitable architecture for a practical prototype board
- Clear, readable engineering notes for EasyEDA or schematic review

## Block diagram

```text
USB-C PD source
      |
      v
+------------------+
| USB-C connector  |
| CC + VBUS + GND  |
+--------+---------+
         |
         v
+------------------+
| ESD / protection |
+--------+---------+
         |
         v
+------------------+
| PD controller    |
| negotiates VBUS  |
+--------+---------+
         |
         v
+------------------+
| DC-DC converter  |
| 5 V to 28 V      |
+--------+---------+
         |
         v
+------------------+
| Output filter    |
| and protection   |
+------------------+
```

## Key implementation notes

- Use a USB Type-C receptacle with the appropriate CC and VBUS routing.
- Include ESD, surge protection, and fuse/TVS protection before the power stage.
- Use a USB PD controller that supports the required voltage profiles.
- Select a DC-DC topology with enough headroom for the complete 5 V to 28 V range.
- Add output regulation, thermal protection, and decoupling capacitors.
- Review the final layout for high-current loops and switching noise mitigation.

## Files in this repo

- `docs/usb-c-power-supply-design.md` — design notes and architecture details
- `schematic/usb-c-power-supply.sch` — concept schematic draft

## Reference

- Robert Feranec: "How to design a USB-C Power Supply (5V to 28V) in 3 hours"
- USB-C Power Delivery specification

This repository is intentionally lightweight and acts as a practical starting point for a real hardware design, not a final manufacturing package.
