<a name="readme-top"></a>

<h1 align="center">
  <br> STM32H743ZI LwIP BareMetal <br>
</h1>

<div align="center">

[![Orel138 - STM32H743ZI_LwIP_BareMetal](https://img.shields.io/static/v1?label=Orel138&message=STM32H743ZI_LwIP_BareMetal&color=blue&logo=github)](https://github.com/Orel138/STM32H743ZI_LwIP_BareMetal "Go to GitHub repo")
[![stars - STM32H743ZI_LwIP_BareMetal](https://img.shields.io/github/stars/Orel138/STM32H743ZI_LwIP_BareMetal?style=social)](https://github.com/Orel138/STM32H743ZI_LwIP_BareMetal)
[![forks - STM32H743ZI_LwIP_BareMetal](https://img.shields.io/github/forks/Orel138/STM32H743ZI_LwIP_BareMetal?style=social)](https://github.com/Orel138/STM32H743ZI_LwIP_BareMetal)

[![Open in Visual Studio Code](https://img.shields.io/static/v1?logo=visualstudiocode&label=&message=Open%20in%20Visual%20Studio%20Code&labelColor=2c2c32&color=007acc&logoColor=007acc)](https://open.vscode.dev/Orel138/STM32H743ZI_LwIP_BareMetal)
[![license](https://custom-icon-badges.demolab.com/github/license/Orel138/STM32H743ZI_LwIP_BareMetal?logo=law&logoColor=white)](https://github.com/Orel138/STM32H743ZI_LwIP_BareMetal/blob/main/LICENSE "license MIT")
[![issues](https://custom-icon-badges.demolab.com/github/issues-raw/Orel138/STM32H743ZI_LwIP_BareMetal?logo=issue)](https://github.com/Orel138/STM32H743ZI_LwIP_BareMetal/issues "issues")

[![STM32](https://img.shields.io/badge/STM32-message?style=flat&logo=stmicroelectronics&color=%2303234B)](https://st.com "STM32")
[![LwIP](https://img.shields.io/badge/LwIP-message?style=flat&color=%23808000)](http://savannah.nongnu.org/projects/lwip/ "LwIP")

</div>

<div align="center">
  <h4>
    <a href="#about">About</a> |
    <a href="#key-goals">Key Goals</a> |
    <a href="#architecture-overview">Architecture</a> |
    <a href="#requirements">Requirements</a> |
    <a href="#installation">Installation</a> |
    <a href="#usage">Usage</a> |
    <a href="#branches">Branches</a> |
    <a href="#references">References</a> |
    <a href="#license">License</a>
  </h4>
</div>

<div align="center">
  <sub>Built by
  <a href="https://orel138.github.io">Orel138</a> and
  <a href="https://github.com/orel138/STM32H743ZI_LwIP_BareMetal/graphs/contributors">contributors</a>
</div>
<br>

## About

**STM32H743ZI LwIP BareMetal** is a lightweight LwIP (Light Weight Internet Protocol) template project for the STM32H743ZI microcontroller on the NUCLEO-H743ZI board. This project demonstrates how to configure and use the LwIP stack in a bare-metal environment with STM32CubeMX, enabling network connectivity with automatic DHCP address assignment.

The default implementation provides a solid foundation for network-enabled embedded applications. The device automatically configures itself on the network via DHCP and responds to ping requests. Additional branches extend this functionality with advanced networking features such as mDNS (Multicast DNS) and DNS-SD (Service Discovery) for seamless service announcement and discovery on local networks.

## Table of Contents

- [About](#about)
- [Key Goals](#key-goals)
- [Architecture Overview](#architecture-overview)
- [Project Structure](#project-structure)
- [Design Principles](#design-principles)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Branches](#branches)
- [References](#references)
- [Contributing](#contributing)
- [License](#license)

## Key Goals

- Provide a ready-to-use LwIP template for STM32H743ZI projects
- Demonstrate basic network connectivity with automatic DHCP configuration
- Ensure compatibility with STM32CubeMX and HAL libraries
- Offer a foundation for network-enabled embedded applications
- Support advanced networking features through dedicated branches (mDNS, DNS-SD)

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Architecture Overview

### High-Level Architecture

```
STM32H743ZI Ethernet Interface
        │
        ▼
LwIP Network Stack
        │
        ▼
DHCP Client (Automatic IP Assignment)
        │
        ▼
Network Services (Ping, mDNS*, DNS-SD*)
        
* Available on "with_mdns" branch
```

### Project Structure

```
.
├── Core/
│   ├── Inc/                 # Core header files
│   │   ├── main.h
│   │   ├── stm32h7xx_hal_conf.h
│   │   └── stm32h7xx_it.h
│   └── Src/                 # Core source files
│       ├── main.c
│       ├── stm32h7xx_hal_msp.c
│       ├── stm32h7xx_hal_timebase_tim.c
│       ├── stm32h7xx_it.c
│       └── system_stm32h7xx.c
│
├── Drivers/
│   ├── CMSIS/               # ARM Cortex-M CMSIS headers
│   │   ├── Device/
│   │   └── Include/
│   └── STM32H7xx_HAL_Driver/# STM32 HAL drivers
│       ├── Inc/
│       └── Src/
│
├── LWIP/
│   ├── App/                 # LwIP application layer
│   │   ├── lwip.c
│   │   └── lwip.h
│   └── Target/              # LwIP configuration and interface
│       ├── ethernetif.c
│       ├── ethernetif.h
│       └── lwipopts.h       # LwIP configuration options
│
├── Middlewares/
│   └── Third_Party/
│       └── LwIP/            # LwIP core library
│
├── STM32CubeIDE/
│   ├── STM32H743ZI_LwIP_BareMetal.launch
│   ├── STM32H743ZITX_FLASH.ld
│   ├── STM32H743ZITX_RAM.ld
│   ├── Drivers/
│   ├── Middlewares/
│   └── Debug/
│
└── README.md                # This file
```

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Design Principles

- **HAL-based Configuration**: Leverages STM32CubeMX and HAL libraries for peripheral initialization
- **Bare-Metal Architecture**: Runs without a Real-Time Operating System (RTOS) for minimal overhead
- **Automatic Network Configuration**: DHCP client automatically assigns IP address on startup
- **LwIP Stack Integration**: Lightweight protocol stack for efficient network operations
- **Modular Design**: Separates network interface, application, and HAL layers for flexibility
- **Extensibility**: Clean foundation for adding protocol extensions (mDNS, DNS-SD, etc.)

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Requirements

### Hardware

- **NUCLEO-H743ZI** Development Board
- Ethernet cable and network connection
- ST-Link/V2 debugger (integrated on Nucleo board)
- Power supply (USB or external)

### Software

- **STM32CubeIDE** (or compatible STM32 toolchain)
- **STM32CubeMX** (for project configuration)
- **STM32Cube MCU Package** for H7 series
- **LwIP** middleware library
- Git (for version control)

### Development Environment

- Windows, Linux, or macOS
- STM32CubeIDE or VS Code with STM32 extension
- Serial terminal utility (for debugging via UART)

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Installation

### Clone the Repository

```bash
git clone https://github.com/Orel138/STM32H743ZI_LwIP_BareMetal.git
cd STM32H743ZI_LwIP_BareMetal
```

### Import into STM32CubeIDE

1. Open **STM32CubeIDE**
2. Select **File** → **Import...**
3. Choose **Existing Projects into Workspace**
4. Browse to the cloned repository directory
5. Click **Finish**

### Build the Project

1. Right-click the project in **Project Explorer**
2. Select **Build Project**
3. Wait for the build to complete successfully

### Flash the Firmware

1. Connect the NUCLEO-H743ZI board via USB
2. Right-click the project in **Project Explorer**
3. Select **Run As** → **STM32 C/C++ Application**
4. Alternatively, use the **Debug** button to flash and debug

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Usage

### Default Behavior

Once flashed and powered on, the device will:

1. **Initialize Ethernet Interface**: Configure the Ethernet MAC and PHY (LAN8742 on NUCLEO-H743ZI)
2. **Start DHCP Client**: Request IP address from DHCP server
3. **Assign IP Address**: Configure network interface with obtained IP
4. **Wait for Requests**: Respond to network requests (e.g., ICMP ping)

### Testing Network Connectivity

#### Ping the Device

After the device boots and obtains an IP address via DHCP, you can test connectivity:

```bash
# On Windows
ping <device-ip>

# On Linux/macOS
ping <device-ip>
```

Replace `<device-ip>` with the IP address assigned by your DHCP server.

#### Monitor via Serial Port

Connect a USB-to-UART adapter to view debug messages from the device:

- **Baudrate**: 115200
- **Data Bits**: 8
- **Stop Bits**: 1
- **Parity**: None
- **Flow Control**: None

### Finding the Assigned IP Address

The IP address assigned by DHCP can be found through:

1. **DHCP Server Logs**: Check your router or DHCP server logs
2. **Network Scanning Tools**: Use tools like `arp-scan`, `nmap`, or your router's web interface
3. **Serial Debugging**: Configure debug output in [LWIP/Target/lwipopts.h](LWIP/Target/lwipopts.h) for IP address logging

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Branches

### master (Default)

Basic LwIP template with DHCP client and ping support. Suitable for projects requiring fundamental network connectivity.

**Features**:
- ✅ Ethernet connectivity
- ✅ DHCP IP address assignment
- ✅ ICMP ping response
- ✅ Bare-metal architecture

### with_mdns

Extended network functionality with mDNS (Multicast DNS) and DNS-SD (Service Discovery) support. Devices on this branch automatically announce themselves on the local network.

**Features**:
- ✅ All master branch features
- ✅ mDNS hostname resolution
- ✅ DNS-SD service announcement
- ✅ Local network discovery (.local domain)
- ✅ Zero-configuration networking (Zeroconf)

**Usage**:

```bash
# Switch to with_mdns branch
git checkout with_mdns

# Rebuild the project
```

After flashing this branch, the device will be discoverable via:

```bash
# Resolve device hostname
ping device-name.local

# Discover services (on Linux/macOS with avahi-tools)
avahi-browse -a
```

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Configuration

### LwIP Options

LwIP configuration is managed in [LWIP/Target/lwipopts.h](LWIP/Target/lwipopts.h). Key options include:

- `LWIP_DHCP`: Enable/disable DHCP client (enabled by default)
- `LWIP_ICMP`: Enable/disable ICMP protocol (ping support)
- `LWIP_UDP`: Enable/disable UDP protocol
- `LWIP_TCP`: Enable/disable TCP protocol
- `MEM_SIZE`: Memory pool size for LwIP

### Ethernet Interface

The ethernet interface is configured in [LWIP/Target/ethernetif.c](LWIP/Target/ethernetif.c). The implementation handles:

- Ethernet MAC initialization
- PHY configuration (LAN8742)
- Packet transmission and reception
- Link status monitoring

### STM32CubeMX Configuration

To modify hardware configuration:

1. Open [STM32H743ZI_LwIP_BareMetal.ioc](STM32H743ZI_LwIP_BareMetal.ioc) with STM32CubeMX
2. Adjust peripheral settings as needed (Ethernet, GPIO, Clocks, etc.)
3. Generate code: **Project** → **Generate Code**
4. Rebuild in STM32CubeIDE

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## References

- [STM32Cube MCU Overall Offer](https://github.com/STMicroelectronics/STM32Cube_MCU_Overall_Offer)
- [LwIP Project](http://savannah.nongnu.org/projects/lwip/)
- [LwIP Documentation](https://lwip.wikia.com/)
- [STM32H743 Reference Manual](https://www.st.com/resource/en/reference_manual/rm0433-stm32h742-stm32h743-753-and-stm32h750-value-line-advanced-arm-based-32-bit-mcus-stmicroelectronics.pdf)
- [NUCLEO-H743ZI User Manual](https://www.st.com/resource/en/user_manual/um1974-nucleo144-board-with-stm32h743zi-mcu-stmicroelectronics.pdf)
- [mDNS/DNS-SD Specifications](https://www.ietf.org/rfc/rfc6762.txt)

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes with clear messages (`git commit -m 'Add your feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## License

This project is released under the [MIT License](LICENSE).

© [Orel138](https://github.com/Orel138)

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

> [!TIP]
> If you find this project useful, consider giving it a ⭐.
> It is the simplest way to show support and helps the project grow.
