# CIT 386 — Module 3 — Assignment 3.1

## Hyper-V Build Log and Disk Behavior

### 1\. Host workstation and lab environment

The VM was managed from a school laboratory workstation through Hyper-V Manager, connected to a remote Hyper-V server at `192.168.82.5`.

|Item|Recorded information|
|-|-|
|Windows edition reported by local PowerShell|Windows 10 Pro (verify: reported build 26200 is associated with Windows 11)|
|Windows build reported|26200|
|Workstation processor|Intel Core i7-14700T, 20 physical cores, 28 logical processors|
|Workstation RAM|15.69 GiB|
|Hyper-V availability|Hyper-V Manager already available in the lab; connected to remote host|
|Remote Hyper-V server|`192.168.82.5`|

**Scope note:** The workstation specifications above came from the school computer's local PowerShell output. They are not verified specifications of the separate Hyper-V server. I did not enable the Hyper-V role myself; management access was already provided in the laboratory.

### 2\. Virtual machine configuration

|Setting|Value|
|-|-|
|VM name|`argin-lilagan`|
|Guest operating system|Ubuntu Server (exact release not recorded)|
|Generation|1|
|Startup memory|4096 MiB (4 GiB)|
|Dynamic memory|Disabled|
|Virtual processor count|14|
|Virtual switch|`vswitch1`|
|Disk controller|IDE Controller 0|
|Virtual disk format|VHDX|
|Disk type|Not verified from host; dynamically expanding **assumed for simulated comparison**|
|Configured disk capacity|Not verified from host; **60 GiB assumed for simulated comparison**|
|VM state|Running|
|Guest IP address|`192.168.82.7`|

**Recorded virtual disk path (on the Hyper-V server):**

`C:\\ProgramData\\Microsoft\\Windows\\Virtual Hard Disks\\argin-lilagan.vhdx`

### 3\. Generation selection

The lab VM was configured as **Generation 1**, which uses legacy BIOS boot and supports older operating systems and virtual hardware. Generation 2 offers UEFI firmware, Secure Boot support, and a more modern virtual hardware model, but it requires a compatible guest operating system and boot configuration. Modern Ubuntu Server releases generally support Generation 2, so Generation 1 was not necessarily required; it was the configuration available for this lab VM. **For the defense checkpoint, explain in your own words why this was the configuration you used.**

### 4\. Measurement method and approved substitution

The lab account did not have the host permissions required to inspect the VHDX file or measure its size on the remote Hyper-V server. My professor approved the use of **simulated disk measurements** because the required host-side information was inaccessible.

The table below is therefore a **hypothetical example**, not data collected from my VM. The figures represent **host-side VHDX file sizes** in a plausible scenario, not Ubuntu guest free-space readings. The example assumes a 60 GiB virtual disk and a 2 GiB guest write. The values after deletion assume no immediate VHDX reclamation; actual behavior depends on the filesystem, discard/TRIM support, and Hyper-V configuration.

### 5\. Simulated disk comparison

|Measurement|Dynamically expanding VHDX (simulated)|Fixed-size VHDX (simulated)|
|-|-:|-:|
|Configured virtual capacity|60.00 GiB|60.00 GiB|
|Host file size before test write|8.42 GiB|60.00 GiB|
|Data written inside guest|2.00 GiB|2.00 GiB|
|Host file size after write|10.46 GiB|60.00 GiB|
|Host file size after guest deletion|10.46 GiB|60.00 GiB|

**Example expectation before deletion:** I would predict that deleting the guest file might free space *inside Ubuntu* but would not necessarily shrink the VHDX file on the host.

**Example outcome, not an observation:** The simulated dynamic VHDX remains at 10.46 GiB after deletion. This illustrates that deleting a file in the guest does not automatically guarantee that allocated VHDX blocks are returned to the host. Automatic reclaim may occur in other configurations, so the result is not universal.

### 6\. Twelve-VM capacity example

For twelve identically configured VMs, the simulated dynamic disks would occupy `12 × 8.42 = 101.04 GiB` initially, compared with `12 × 60 = 720 GiB` for the simulated fixed disks. After the example write, twelve dynamic disks would occupy `12 × 10.46 = 125.52 GiB`; however, they could continue growing toward their configured capacities, so the host must plan for that risk. Fixed disks can be useful when reserving capacity in advance and avoiding unexpected growth are important; this is a **sample interpretation for review**, not a claim about measured lab performance.

### 7\. Limitations and AI disclosure

* **Verified:** Local workstation information, VM settings visible in Hyper-V Manager, running Ubuntu guest, and the displayed VHDX path.
* **Not verified:** Actual Hyper-V server specifications, configured VHDX capacity, actual disk type, and all host VHDX size measurements.
* **Instructor-approved substitution:** All numerical disk comparison readings are simulated and explicitly labeled.
* **AI assistance:** ChatGPT (OpenAI) helped explain Hyper-V settings and format this Markdown document, and produced the clearly labeled simulated example figures and sample explanations. The student should review and revise the interpretation in their own words for the defense checkpoint. The Git commit message must also disclose this assistance.

