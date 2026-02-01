# Device Images and Licensing Guidance

This document explains how **open-network-labs** handles device images and licensing.

The goal is to enable realistic, vendor-specific labs while keeping this repository
legally clean and easy to distribute.

---

## Core Policy

- Proprietary network operating system images are **not** included in this repository
- Contributors must **not** upload or link to proprietary images or unofficial downloads
- Labs may reference vendor-specific platforms, but users must obtain images themselves
  through official channels

This policy applies uniformly to all vendors.

---

## Why This Matters

Most commercial network operating systems are licensed software.
Redistributing them — even unintentionally — can violate licensing terms.

By keeping images out of the repository:
- contributors are protected
- users remain responsible for their own entitlements
- the project can remain openly accessible

---

## What Lab Authors Should Do

When writing a lab that depends on a proprietary platform:

1. **Name the platform and version clearly**
2. **Reference only official vendor documentation or portals**
3. **Provide high-level build or import notes**, if helpful
4. **Do not include the image itself**

Keep instructions factual and neutral.

---

## Example Image Documentation Section

Include a section like this in your lab README:

**Images**
- Platform: Cisco IOL (containerized via vrnetlab)
- Image source: Cisco official download portal (user entitlement required)
- Notes: Image must be built locally using vrnetlab before deploying the lab

Avoid embedding links to files or archives.

---

## Common Platforms Used in Labs

### Open-Source Platforms
These may be referenced freely and, where appropriate, pulled automatically:

- FRRouting (FRR)
- Linux-based routing containers
- Utility containers (e.g., netshoot)

### Vendor-Specific Platforms (User-Supplied)
These may be used **only if obtained by the user through official channels**:

- Arista cEOS
- Cisco IOL / IOU (containerized via vrnetlab)
- Other containerized or virtual network operating systems

The repository must never include the images themselves.

---

## vrnetlab and Local Builds

Tools like **vrnetlab** allow users to build container images locally
from vendor-supplied files they are licensed to use.

It is acceptable to:
- mention vrnetlab as a build mechanism
- describe the general workflow at a high level

It is **not** acceptable to:
- include vendor files
- link to unofficial image sources
- document steps intended to bypass licensing restrictions

---

## What Not to Do

Do not:
- upload qcow2, vmdk, bin, ova, tar, or similar files
- commit exported Docker images
- link to third-party mirrors or file-sharing sites
- suggest workarounds for access or licensing requirements

If in doubt, err on the side of omission.

---

## Questions

If you are unsure whether an image reference is acceptable:
- open an issue
- ask in discussions
- or request guidance before submitting a pull request

We prefer clarity and caution over cleanup after the fact.
