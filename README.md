# open-network-labs

**open-network-labs** is a community-driven collection of hands-on networking labs, built to help learners progress from fundamental concepts to advanced real-world designs.

The labs are designed to be:
- practical and reproducible
- vendor-agnostic in spirit
- focused on understanding *how networks actually behave*
- usable as standalone learning exercises or as supplements to any certification path

This project is not affiliated with any commercial training provider.


## Project Status

This project is **under active development**.

- The directory structure and lab format are stabilizing
- A small number of exemplar labs are being built first
- Feedback is welcome, but expect some iteration early on

If you’re evaluating this repository early, think of it as a **reference implementation** for how networking labs can be structured in an open, reproducible way.


## Philosophy

These labs are not meant to be “click-by-click” walkthroughs or exam cramming exercises.

Each lab aims to:
- present a realistic but focused topology
- give you a working starting point (“before”)
- define clear outcomes rather than exact commands
- provide configuration, troubleshooting, and analysis options
- encourage exploration, verification, and troubleshooting
- show one *possible* solution ("after"), not the only solution
- provide optional further reading, both internally written and links to external books, blogs, and RFCs

If you can explain *why* the lab works when you’re done, it succeeded.

## Topics Covered

Over time, labs will span areas such as:
- Layer 2 switching
- Layer 3 routing
- Interior and exterior routing protocols
- Redundancy and convergence
- Policy and traffic control
- Overlays and underlays
- Troubleshooting and failure analysis
- Automation and observability
- Security


## Requirements

Labs are built using:
- [containerlab](https://containerlab.dev/)
- [labhost-lite](https://github.com/CapnCheapo/labhost-lite) a freely-available docker container to simulate end-hosts.
- containerized network operating systems or routing stacks

Each lab README documents what images are required.

## Where to Start

See `docs/getting-started.md` for help installing the prerequisites needed to run these labs.

Check out `docs/learning-paths` for curated lists of topics sorted by category. The `basic-connectivity` configuration lab is the perfect starting point for 
new and seasoned network professionals alike.

## Contributing

Contributions are welcome, but structure matters.

Before submitting a lab, please:
- follow the established directory layout
- include a complete starter and solution
- clearly document objectives and verification steps
- avoid copying proprietary or copyrighted material

See `CONTRIBUTING.md` for details.


## Why This Exists

Networking knowledge is best learned by *building, breaking, and fixing*.

This project exists to:
- lower the barrier to serious hands-on practice
- provide reusable, transparent lab designs
- create a shared commons of networking understanding

If you learn something while building a lab here, the project is working.
