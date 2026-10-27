# WK1-PM1: Cybersecurity Testing Lab Setup

**Name:** Julia
**Date:** 27 October 2026

## Environment
- Host: Windows 10 laptop (Acer)
- Hypervisor: Oracle VirtualBox 
- Attacker VM: Kali Linux, VM name `kali`

## Configuration
| Requirement | Setting |
|---|---|
| Network type | NAT Network named `LabNet` |
| Subnet | 10.0.0.0/24 (gateway 10.0.0.1, DHCP off) |
| Kali IP | 10.0.0.2/24 (static, set with nmcli) |
| Internet access | Working (ping google.com succeeds) |
| Clipboard | Bidirectional |
| Drag and Drop | Bidirectional |
| Shared folder | Windows Downloads, mounted at /media/sf_Downloads |

## Steps taken
1. Created the NAT Network: `VBoxManage natnetwork add --netname LabNet --network "10.0.0.0/24" --enable --dhcp off`
2. Attached Adapter 1 of the kali VM to NAT Network `LabNet`.
3. Set Shared Clipboard and Drag'n'Drop to Bidirectional.
4. Added the Windows Downloads folder as a shared folder (Auto-mount, Make Permanent).
5. Installed Guest Additions: `sudo apt install virtualbox-guest-x11 virtualbox-guest-utils`
6. Set the static IP with `nmcli con mod` and `nmcli con up`.

## Verification (see screenshots)
- `ip a` shows 10.0.0.2/24 on eth0
- `ping -c 3 google.com` succeeds
- `ls /media/sf_Downloads` lists the Windows Downloads files
- Clipboard copy/paste works in both directions

## Issues and fixes
- **apt "Malformed line 1 in sources.list":** rewrote /etc/apt/sources.list with the correct Kali repository line.
- **Shared folder not mounting:** mounted manually with `mount -t vboxsf`, then enabled Auto-mount.
- **Drag and drop:** enabled in settings but very slow, so files were moved through the shared folder instead.

## Screenshots
1. ...
