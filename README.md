# Mobile Device Management (MDM) with iOS — Microsoft Intune + Entra ID

**Platform note:** This lab was performed on iOS. The same concepts apply to other mobile platforms.

## Overview

This project demonstrates a modern Mobile Device Management (MDM) workflow using **Microsoft Intune** and **Microsoft Entra ID**:

- Enroll an iPhone into Intune with Company Portal
- Enforce a **baseline compliance policy** (passcode, no jailbreak, encryption)
- Apply an **iOS configuration profile** (core restrictions)
- **Publish Outlook** to the managed device
- Verify device sync/compliance in Intune


---

## What I built

- **Entra ID test user:** `IOS_user` (Display name: *IOS Test User*)
- **Groups:** used a dedicated device-targeting group (e.g., `MDM-iOS-Users`) for clean scoping
- **Compliance policy:** iOS baseline security (PIN required, block jailbreak, etc.)
- **Configuration profile:** iOS device restrictions (disable iCloud backup for managed data, enforce encrypted backups, etc.)
- **App deployment:** Outlook from the Apple App Store to enrolled devices

---

## Step-by-step

### 1) Create iOS Test User & Group Targeting
Created `IOS_user` in Entra ID and assigned an Intune license. Added the user to an iOS-specific Intune group for policy targeting.

<p align="center">
User & Group Setup<br/>
<img src="https://i.imgur.com/To9Nsvf.png" width="800" style="height:auto;" alt="Entra ID user and group membership"/>
<br /><br />
</p>

___

### 2) Configure Apple MDM Push Certificate
Completed the Apple Push Certificate workflow so Intune can manage iOS devices (download CSR from Intune → upload to Apple → upload resulting certificate back to Intune).

<p align="center">
Apple MDM Push Certificate Connected<br/>
<img src="https://i.imgur.com/oUFQrKk.png" width="800" style="height:auto;" alt="Apple MDM push certificate connected in Intune"/>
<br /><br />
</p>

___

### 3) Enroll iPhone with Company Portal
Installed **Company Portal** on the iPhone and signed in with `IOS_user`. Completed the enrollment prompts so the device is registered and manageable.

<p align="center">
Enrollment Complete (Company Portal) <br/>
<img src="https://i.imgur.com/YZi2148.png" width="800" style="height:auto;" alt="Company Portal showing the device is enrolled"/>
<br /><br />
</p>

___

### 4) Create iOS Compliance Policy — Baseline Security
Policy scope: `MDM-iOS-Users`. Key requirements:
- Jailbroken devices: **Blocked**
- Require passcode/PIN to unlock
- Block simple passwords; minimum length set
- Encryption required (where supported)

<p align="center">
Compliance Policy — Review<br/>
<img src="https://i.imgur.com/1N9vmGW.png" width="800" style="height:auto;" alt="Intune iOS compliance policy review screen"/>
<br /><br />
</p>

___

### 5) Create iOS Configuration Profile — Device Restrictions
Profile scope: `MDM-iOS-Users`. Representative settings:
- Disable iCloud backup for managed data
- Require encrypted backups
- Enforce passcode complexity (no simple PIN)
- Limit unmanaged data flows (e.g., AirDrop as unmanaged destination)

<p align="center">
Configuration Profile — Review<br/>
<img src="https://i.imgur.com/OTmkkUp.png" width="800" style="height:auto;" alt="Intune iOS device restrictions profile review screen"/>
<br /><br />
</p>

___

### 6) Publish Outlook (iOS Store App)
Added **Microsoft Outlook** (iOS store app) in Intune and assigned it to the iOS group.

<p align="center">
Outlook Available in Company Portal<br/>
<img src="https://i.imgur.com/Yroit6g.png" width="800" style="height:auto;" alt="Company Portal showing Outlook recently published for this device"/>
<br /><br />
</p>

___

### 7) Sync & Verify
Forced a sync in Company Portal, then verified device and policy status in the Intune admin center.

<p align="center">
Intune Device Sync & Compliance View<br/>
<img src="https://i.imgur.com/8tSsBBj.png" width="600" style="height:auto;" alt="Intune showing device compliance/sync status"/>
<br /><br />
</p>

---

## What I learned

- How **Intune (MDM)** and **Entra ID** integrate to manage mobile endpoints
- Enforcing **compliance** and **configuration** on iOS at scale
- Publishing approved apps (Outlook) to enrolled devices
- Verifying device state and troubleshooting enrollment/licensing issues

