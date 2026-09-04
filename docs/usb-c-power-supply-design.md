# USB-C Power Supply Design Notes

## Objective

Design a USB-C power source that can negotiate and deliver an adjustable output from 5 V up to 28 V while remaining practical for a compact lab-style or portable supply.

## Core idea

Use a USB-C receptacle and PD controller to accept a negotiated power profile from a USB PD source, then feed a switch-mode converter that produces the required output voltage. The design uses a PD-aware front end and a configurable conversion stage instead of a fixed-output regulator.

## Signal and power path

```text
USB-C VBUS --- ESD / TVS --- PD controller --- DC-DC regulator --- Output filter --- 5V..28V rail
             \                    /                    /
              `----- CC / protection ------------------'
```

## Detailed block breakdown

### 1. USB-C receptacle and protection

- Connect VBUS, GND, CC1, and CC2 as required for Type-C operation
- Include ESD protection on the USB lines and VBUS input
- Add a fuse or resettable polyfuse where appropriate for fault protection
- Keep the connector area free of unnecessary routing congestion

### 2. USB PD negotiation

- Implement a PD controller that can announce and accept the desired voltage profile
- Validate source capabilities and required PDOs
- Make sure the converter input rail is stable while the PD contract is changing

### 3. Power conversion

- Choose a switch-mode solution with enough margin for the highest required output power
- Evaluate buck-only, boost-only, and buck-boost topologies based on the final output range
- Ensure the inductor, FETs, and diode/synchronous rectifier are selected for efficiency and temperature

### 4. Output stage

- Add bulk capacitance and ceramic decoupling near the converter output
- Include voltage sensing and feedback division for output regulation
- Add output overcurrent and thermal protection for safe operation

### 5. Layout strategy

- Keep the PD controller close to the USB-C connector
- Place high-current switching components together to minimize loop area
- Route the power path on wider copper pours and avoid long thin traces
- Separate noisy switching nodes from sensitive analog/feedback nodes

## Recommended design checklist

- Confirm USB-C PD source compatibility
- Define max output current and power
- Choose a converter topology that supports 5 V to 28 V range
- Check MOSFET and inductor thermal conditions
- Validate transient response and startup behavior
- Measure EMI and thermal performance in the prototype

## Practical notes

This design is meant to be a solid reference for a prototype or in-progress board. A production-quality version should be reviewed against the selected controller and power-stage datasheets, plus relevant USB-C PD compliance requirements.
