
---

# Network Driver Installation Guide

This guide will walk you through installing network drivers on both **Windows** and **Linux** systems.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Installing Network Drivers on Windows](#installing-network-drivers-on-windows)
3. [Installing Network Drivers on Linux](#installing-network-drivers-on-linux)
4. [Troubleshooting](#troubleshooting)

---

## Prerequisites

Before installing network drivers, ensure you have:
- The correct driver files for your network card (download from the manufacturer's website or have them stored on a USB drive).
- Administrator or root access to the system.
- A working USB or disk with the drivers if your system is offline.

---

## Installing Network Drivers on Windows

### Step 1: Download the Driver
1. Visit your network adapter manufacturer's website (e.g., Intel, Realtek, Broadcom).
2. Search for the latest drivers compatible with your version of Windows.
3. Download the `.exe` file or `.zip` containing the driver.

### Step 2: Install the Driver
1. **Run the Installer**:
   - If the driver is an `.exe` file, double-click it to launch the installer and follow the on-screen instructions.
2. **Extract and Install**:
   - If the driver is in a `.zip` file:
     - Right-click on the `.zip` file and select "Extract All."
     - Open Device Manager by right-clicking on the Start menu and selecting **Device Manager**.
     - In Device Manager, expand **Network adapters**.
     - Right-click on your network adapter and select **Update Driver**.
     - Choose **Browse my computer for driver software**.
     - Navigate to the folder where you extracted the driver and click **Next**.

### Step 3: Reboot Your System
- After installation, restart your computer to complete the installation and ensure the network adapter functions properly.

---

## Installing Network Drivers on Linux

### Step 1: Identify Your Network Adapter
Open a terminal and run the following command to list your network interfaces and adapters:

```bash
lspci | grep -i network
```

This will return details about your network card (e.g., Intel, Realtek).

### Step 2: Install Required Packages (for most distros)
Update your system's package list and install any dependencies that may be required to compile drivers:

```bash
sudo apt-get update
sudo apt-get install build-essential linux-headers-$(uname -r)
```

### Step 3: Download and Install the Driver
#### Option 1: Using Package Managers
1. If your network driver is available via a package manager (e.g., for Intel cards):

   ```bash
   sudo apt-get install firmware-iwlwifi
   ```

2. After installation, reload the kernel module:

   ```bash
   sudo modprobe -r iwlwifi
   sudo modprobe iwlwifi
   ```

#### Option 2: Installing from Source
1. Download the driver from the manufacturer’s website (e.g., Realtek, Broadcom).
2. Extract the contents of the `.tar.gz` or `.zip` file.
3. Open a terminal and navigate to the extracted directory:

   ```bash
   cd /path/to/extracted/driver
   ```

4. Compile and install the driver:

   ```bash
   make
   sudo make install
   ```

5. Reboot your system:

   ```bash
   sudo reboot
   ```

### Step 4: Verify Installation
Once the system restarts, check if the driver is installed correctly by running:

```bash
sudo lshw -C network
```

---

## Troubleshooting

### Windows
- If the driver installation fails, make sure you're installing the correct version of the driver for your Windows version (e.g., Windows 10 64-bit).
- **Error Codes in Device Manager**: If you see error codes in Device Manager after installing the driver, you may need to roll back the driver or try a different version from the manufacturer's website.

### Linux
- If the network card is still not recognized, ensure that `secure boot` is disabled in your BIOS/UEFI settings. Some drivers require this.
- **Driver Compilation Issues**: If you're building the driver from source and encounter errors during `make`, check the documentation provided with the driver for dependencies you may have missed.

---

## Additional Resources
- [How to Identify Network Hardware on Linux](https://linuxhint.com/check_network_adapter_linux/)
- [Official Realtek Drivers for Windows](https://www.realtek.com/en/component/zoo/category/network-interface-controllers-10-100-1000m-gigabit-ethernet-pci-express-software)
- [Intel Wireless Drivers & Software](https://www.intel.com/content/www/us/en/support/products/189347/network-and-i-o/wireless-networking.html)

