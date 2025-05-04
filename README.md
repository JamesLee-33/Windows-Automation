Hyper-V Host Deployment – Setup

📝 Overview

This document outlines the real-world deployment of a Hyper-V environment

Environment Details

Host OS: Windows Server 2022 Standard

Hardware: Dell PowerEdge R730

Memory: 128 GB RAM

Storage: 4 × 1.2TB SAS drives (RAID 10 via PERC controller)

Hypervisor Role: Installed via Server Manager GUI

VM Storage Path: D:\VMs\

Networking:

External vSwitch mapped to physical NIC

VLAN tagging configured at switch level

⚙️ Installation Process

1. Installed Hyper-V Role

Install-WindowsFeature -Name Hyper-V -IncludeManagementTools -Restart

2. Configured Virtual Switch

Created an external virtual switch bound to NIC1

Left "Allow management OS to share this adapter" enabled

Reserved NIC2 for future Proxmox experiments or iSCSI

3. Default Settings Modified

Moved default VM storage location to high-speed RAID volume

Enabled Enhanced Session Mode

Disabled automatic checkpoints (manual checkpoints only)

4. Provisioned Initial VMs

VM 1: Domain Controller (Windows Server 2019)

VM 2: File Server (Windows Server 2022)

VM 3: Lightweight Ubuntu test VM for Wazuh testing

🔐 Security & Management

Enabled Windows Defender AV and Firewall on host

Configured nested virtualization on Ubuntu VM

Used PowerShell to enforce VM memory limits

Snapshots disabled in production VM environments

RDP access restricted by firewall and NSG rules

📚 Lessons Learned

Default Hyper-V switch config routes all traffic unless you segment VLANs explicitly

Storage location changes must be configured before first VM creation to avoid migration hassle

Nested virtualization performance varies based on CPU model — not all BIOS settings apply

Hyper-V firewall rules need manual confirmation if PowerShell is used instead of GUI

📈 Next Steps

Migrate internal test VMs to Proxmox lab (when hardware arrives)

Document networking configs to mirror Azure NSG behavior

Create baseline templates for future Hyper-V → Azure lift-and-shift simulations

📄 This file:

Looks professional

Documents real experience

Shows planning and operational awareness

Is immediately useful for your portfolio and GitHub

