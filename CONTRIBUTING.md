# Contributing to open-network-labs

Thank you for your interest in contributing to **open-network-labs**.

This project exists to build a shared, high-quality collection of hands-on networking labs.
Structure, clarity, and reproducibility matter more than volume.

---

## What Makes a Good Contribution

A good lab:
- focuses on a specific concept or closely related set of concepts
- is self-contained and reproducible
- includes a clear starting point and a working solution
- verifies outcomes rather than exact configuration syntax
- teaches through observable behavior, not memorization

If your lab helps someone understand *why* a network behaves the way it does, it belongs here.

---

## Required Repository Structure

All labs **must** follow this structure:

```
lab-name/
├── lab.meta.yml
├── starter/
│ ├── topology.clab.yml
│ ├── configs/
│ └── README.md
├── solution/
│ ├── topology.clab.yml
│ ├── configs/
│ └── README.md
└── check/ # optional
└── validate.*
```

Submissions that do not follow this structure may be requested to be revised.

---

## Lab Metadata

Each lab must include a `lab.meta.yml` file with, at minimum:

- `title`
- `summary`
- `topics`
- `difficulty` (1–5)
- `estimated_time`
- `prerequisites`
- `outcomes`

Metadata should describe **what the learner gains**, not what commands they type.

---

## Starter vs Solution

### Starter
The **starter** directory must:
- deploy successfully using containerlab
- include only baseline configuration
- not already satisfy the lab objectives

The learner should have real work to do.

### Solution
The **solution** directory must:
- fully satisfy all lab objectives
- include verification commands
- show example output where practical

The solution represents *one valid approach*, not the only approach.

---

## Validation (Optional but Encouraged)

Validation scripts may be included to:
- confirm reachability
- check protocol state
- verify routes, neighbors, or tables

Validation must:
- test observable outcomes
- avoid brittle text matching when possible
- pass on the solution topology
- fail on the starter topology

---

## Device Images, Licensing, and Downloads (Important)

This repository does **not** include proprietary network operating system images (or derived artifacts),
and contributors must not add them.

### Allowed
You may contribute labs that use vendor-specific platforms (e.g., Arista cEOS, Cisco IOL via vrnetlab),
as long as the lab:

- does **not** include proprietary images, binaries, or container layers built from them
- documents the required image(s) by name and version
- points users only to **official vendor sources** or official documentation describing how to obtain them

### Not Allowed
Do **not**:
- commit proprietary images, qcow2/vmdk/bin files, or archives containing them
- commit pre-built containers that embed proprietary software (including exported Docker images or tarballs)
- link to third-party mirrors, file-sharing sites, or unofficial downloads
- provide instructions intended to bypass licensing, authentication, or access controls

### Required Documentation Pattern
Each lab README must include an **Images** section that clearly documents image requirements.

Example:

**Images**
- Platform: Arista cEOS 4.x (user-supplied)
- How to obtain: Refer to the vendor’s official download portal or documentation
- Local build notes (optional): brief, high-level steps to import or build the image locally

For additional guidance, see `docs/images.md`.

---

## Supported Platforms

Labs may use any platform supported by containerlab, including:
- open-source routing stacks
- containerized network operating systems
- virtualized network devices

Contributors must **not** include proprietary images in this repository.

---

## Style and Conventions

- Use clear, descriptive lab names
- Keep configurations readable and commented where appropriate
- Prefer clarity over minimalism
- Assume the reader is capable, curious, and learning

---

## Submitting a Contribution

1. Fork the repository
2. Create a feature branch
3. Add or modify a lab following the required structure
4. Verify:
   - starter deploys successfully
   - solution deploys successfully
   - validation (if present) behaves as intended
5. Open a pull request with a clear description of:
   - what the lab teaches
   - what prerequisites it assumes

Maintainers may request revisions to preserve consistency and quality.

---

## Code of Conduct

Be respectful, constructive, and collaborative.

This project welcomes contributors of all experience levels.
Strong ideas matter more than perfect prose.

---

## Questions and Discussion

If you are unsure whether a lab fits:
- open an issue
- start a discussion
- or submit a draft pull request for feedback

We would rather guide a good idea early than reject it late.
