# CIT 386 — Module 4, Assignment 4.1
## Hyper-V Reachability Matrix and VirtualBox Comparison

**Student:** Argin Lilagan  
**Evidence type:** Observed VM configuration plus **instructor-authorized simulated network scenarios and timing values**.  
**Important:** The results below are **not measurements taken on the laboratory machines**. The five targets are illustrative because the original lab's five target definitions were not provided. Replace them if the instructor requires the exact lab targets.

### 1. Observed configuration (from student screenshots)

- VM: `argin-lilagan`, Ubuntu guest, running in Hyper-V Manager on a remote host.
- VM network adapter: `vswitch1`.
- Switch type: **Private**, as reported by the student (the VM adapter settings screenshot shows the switch name but not its type).
- VM resources: 4,096 MB RAM, 14 virtual processors, `argin-lilagan.vhdx` virtual disk.
- Guest had an IPv4 address and DHCP-supplied routes, including a default gateway. **Having a route is not proof of successful reachability.** No actual ping or application-level reachability outcomes were supplied.

### 2. Simulated reachability matrix — not lab measurements

**Simulation assumptions:** VM A is the test guest. VM B is attached to the same virtual switch. Guest IP addressing is correctly configured for each scenario. Firewalls permit ICMP. The physical LAN and internet work when bridged. No NAT or routing is configured for Private or Internal switches. The management OS sharing toggle refers to the host's use of the selected physical adapter, not to the guest's basic external connectivity.

The five **illustrative targets** are: (1) VM B on the same switch, (2) Hyper-V host management OS, (3) physical LAN device, (4) public internet IP, and (5) public DNS hostname.

| Hyper-V switch configuration | VM B (same switch) | Management OS | LAN device | Public IP | Public hostname |
|---|---|---|---|---|---|
| Private | Pass (simulated) | Fail (simulated) | Fail (simulated) | Fail (simulated) | Fail (simulated) |
| Internal | Pass (simulated) | Pass (simulated) | Fail (simulated) | Fail (simulated) | Fail (simulated) |
| External — management OS shares adapter | Pass (simulated) | Pass (simulated) | Pass (simulated) | Pass (simulated) | Pass (simulated) |
| External — management OS does **not** share adapter | Pass (simulated) | **Conditional** | Pass (simulated) | Pass (simulated) | Pass (simulated) |

**External sharing comparison:** The **Management OS** column is the one that changes or becomes conditional. With sharing enabled, Hyper-V normally creates a host-side virtual network adapter connected to that external switch. With sharing disabled, that host-side adapter is not created for the switch; however, the host might still be reachable through another NIC or network route. Therefore, claiming an unconditional failure would be misleading. The guest's LAN/internet access need not change merely because host sharing is toggled.

**Why a result could be surprising:** An Internal switch allows VM-to-host communication but does not automatically give the VM internet access. I might previously have assumed that because the host has internet access, any VM that can reach the host can also reach the internet; that requires NAT or routing configuration.

**Limitations:** This is a theoretical simulation under stated assumptions, not a replacement for observed ICMP or TCP tests. DNS failures, guest firewalls, physical LAN restrictions, alternate host NICs, and routing can produce different real results.

### 3. Hyper-V and VirtualBox mode mapping

| Hyper-V type | Closest VirtualBox mode | Reason |
|---|---|---|
| Private | Internal Network | Allows VMs on the same isolated virtual network to communicate, without a host-side network interface by default. |
| Internal | Host-only Adapter | Connects VMs to one another and to a host-side virtual adapter, without automatic external routing. |
| External | Bridged Adapter | Connects a VM to the physical network through a host NIC. |

**Pairing that does not line up neatly:** VirtualBox **NAT** has no direct one-to-one match among Hyper-V's three basic switch types. Hyper-V can provide NAT by adding host networking and NAT configuration, often using an Internal switch. In addition, Hyper-V External's **management OS sharing** option does not map exactly to a separate VirtualBox networking mode.

### 4. Simulated VirtualBox timing comparison — not benchmark results

**Illustrative workload:** Time from starting the same VirtualBox Ubuntu guest until its login prompt is ready, with the same VM settings, storage, and machine, and no other major workload changes.

| VirtualBox host configuration | Illustrative elapsed time | Status |
|---|---:|---|
| Hyper-V platform off | 38 seconds | Simulated example, not measured |
| Hyper-V platform on | 54 seconds | Simulated example, not measured |

**Two-sentence explanation:** With the Hyper-V platform off, VirtualBox can use the processor's hardware virtualization features through its native virtualization engine. When Hyper-V is active, VirtualBox may instead run through Microsoft's Windows Hypervisor Platform interface, adding a different virtualization layer that can affect performance; the example 16-second difference is illustrative and not evidence of actual performance on the lab machine.

### 5. Safety and submission notes

- No shared Hyper-V virtual switches or host network adapters were changed to generate this simulation.
- The assignment originally requests observed reachability and measured timings; this document uses simulated values **only on the basis of the student's report that the professor approved simulation**.
- If the instructor provides the original five targets or requires a specific test procedure, revise the matrix labels and assumptions accordingly.
- The public resume website and PDF are separate deliverables under `module04/resume/`.

### AI assistance disclosure

ChatGPT assisted with the networking explanation, Markdown formatting, and generation of **clearly labeled simulated** reachability scenarios and timing examples. The student must review the interpretation and disclose this assistance in the Git commit message.
