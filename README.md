# CAN Fuzzing on SavvyCAN using ICSim

This project demonstrates a hands‑on approach to **Controller Area Network (CAN) fuzzing** using **SavvyCAN** and the **Instrument Cluster Simulator (ICSim)**.  
It is designed for learning automotive security concepts and experimenting with fuzzing techniques on a simulated CAN bus environment.

---

## Overview

In automotive security research, **fuzzing** is a technique where random or mutated CAN frames are sent over a CAN network to observe how systems respond. Fuzzing helps uncover unexpected behavior or potential vulnerabilities by generating diverse message patterns.:contentReference[oaicite:1]{index=1}

This repository provides tools, scripts, and configurations to:

- Use **ICSim** to simulate a CAN bus environment  
- Capture CAN traffic from the simulator  
- Inject fuzzed CAN frames using **SavvyCAN**
- Analyze the effects of fuzzing on the CAN network

ICSim is an open‑source **Instrument Cluster Simulator** used to emulate a vehicle dashboard and generate CAN traffic.:contentReference[oaicite:2]{index=2}

---

## Features

- Setup instructions for CAN bus fuzzing via virtual CAN interfaces  
- Fuzzing of selected CAN IDs and data fields  
- Integration with SavvyCAN’s fuzzing tools  
- Analysis of CAN traffic captured from ICSim

---

## Project Structure

```
CAN_fuzzing_on_SavyCAN_using_ICsim/
├── scripts/ # Fuzzing and utility scripts
├── configs/ # Configuration files
├── docs/ # Documentation and notes
├── examples/ # Example CAN logs or setups
├── README.md # Project documentation
└── LICENSE # (Optional) License
```

---

## Prerequisites

To perform CAN fuzzing using this project, make sure you have:

- A **Linux system** with SocketCAN support  
- **can-utils** installed (`candump`, `cansend`, etc.)  
- **SavvyCAN** for CAN traffic analysis and fuzzing  
- **ICSim** (Instrument Cluster Simulator) installed and built from source

Example installation resources:

```bash
sudo apt install can-utils
```

Set up a virtual CAN interface for safe experimentation:
```bash
sudo modprobe can
sudo modprobe vcan
sudo ip link add dev vcan0 type vcan
sudo ip link set up vcan0
```

You should see the interface when running ifconfig or ip addr.

## Usage

### 1. Start the Simulator

Launch ICSim on the virtual CAN interface:

```bash
./icsim vcan0
```
This starts the instrument cluster simulator that generates CAN traffic.
## 2. Connect SavvyCAN

Open SavvyCAN and connect to the `vcan0` interface:

1. File → Open Connection Window  
2. Add New Device Connection → socketcan/vcan0  
3. Save the settings  

---

## 3. Capture and Analyze CAN Traffic

Use SavvyCAN or can-utils tools:

```bash
candump vcan0
```
You can view live CAN frames and inspect message IDs.

## 4. Fuzz CAN IDs

In SavvyCAN’s fuzzing interface:

- Select a target CAN ID or bit range  
- Configure fuzz bit patterns (random, sequential, sweep)  
- Start fuzzing and observe the frames sent to `vcan0`  
- Monitor changes in system behavior or responses  

> **Note:** Fuzzing sends intentionally modified CAN data to test how the simulated bus handles unexpected traffic. Be cautious when applying these techniques to real hardware.

---

## Learning Resources

Here are some useful resources to understand the concepts involved:

- **SavvyCAN Fuzzing Window Documentation** – explains fuzz control options and bit patterns ([SavvyCAN](https://www.savvycan.com/docs/fuzzingwindow.html))  
- **ICSim (Instrument Cluster Simulator) GitHub** – simulator for CAN environment emulation ([GitHub](https://github.com/zombieCraig/ICSim))  
- Blogs and tutorials on CAN bus analysis with SavvyCAN and can-utils ([CSDN Blog](https://blog.csdn.net/We8__/article/details/128441720))  

---

## Safety and Ethics

⚠️ **Important:** Fuzzing real automotive systems can be dangerous and damaging. Never fuzz live vehicles or critical systems unless in a controlled environment and with permission. This project is intended for **simulation and learning purposes only**.

---

## Contributing

Contributions, improvements, or example scenarios are welcome!  
Please open an issue or submit a pull request with clear descriptions of your changes.

---

## Author

**Manasi Tawade**  
GitHub: [https://github.com/Manasi-16-08](https://github.com/Manasi-16-08)



