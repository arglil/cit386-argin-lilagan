# VirtualBox Appliance Export

## Snapshot

I created a snapshot of my CIT386 virtual machine before exporting it. This gives me a way to return the VM to its previous state if needed.

## Export

- VM: `CIT386-VM01`
- Format: Open Virtualization Format 1.0
- Exported file: `CIT386-VM01.ova`
- Exported file size: 3,082,797,568 bytes (about 3.08 GB)

## Checksum

I generated a SHA-256 checksum of the exported appliance using PowerShell.

Command used:

`Get-FileHash "$HOME\OneDrive\misc\Documents\CIT386-VM01.ova" -Algorithm SHA256`

SHA-256:

`C0964BE9A8CF0232B8EB67EAE679987995BCFABBAA7F9F85ECF84D15E27D5747`

## File Size Comparison

- Original VM folder size: 5.99 GB
- Exported appliance size: 3.08 GB

The exported appliance is smaller than the original VM folder. The original folder contains the VM files, snapshots, and other VirtualBox data. The exported appliance packages the files needed to import and run the VM on another computer, so it does not include everything stored in the original VM folder.