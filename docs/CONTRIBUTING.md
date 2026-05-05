---
title: OmniWM Contribution Guide
---

# OmniWM Contribution Guide

This page is the contributor entry point for the docs site. The canonical contribution guide lives in the repository root at [CONTRIBUTING.md](https://github.com/BarutSRB/OmniWM/blob/main/CONTRIBUTING.md).

This page stays short on purpose so the actual project rules only have one source of truth.

## Start Here

- Read the [canonical contribution guide](https://github.com/BarutSRB/OmniWM/blob/main/CONTRIBUTING.md).
- Review the [Architecture Guide](ARCHITECTURE.md) if your change touches core internals, layout behavior, or app structure.
- Review the [IPC & CLI Reference](IPC-CLI.md) if your change affects automation, commands, queries, or scripting.
- For the user-facing overview, installation notes, and screenshots, see the [README](https://github.com/BarutSRB/OmniWM/blob/main/README.md).

## Project Direction at a Glance

- Refactors are welcome when they come with a detailed reason and a clear benefit.
- **C** or **Zig** rewrites are **very welcome** where there is a strong technical reason they fit better.
- Otherwise, keep contributions in Swift.
- Rust rewrites are not a project direction for OmniWM.

## Reliability Transcripts (Phase 05)

If your change touches lifecycle, focus, topology, frame, monitor, or
workspace state, add or update a transcript under
`Tests/OmniWMTests/Transcripts/Goldens/`. The `make transcripts` and
`make verify` targets run the transcript suite plus
`Scripts/check-transcript-coverage.sh`, which fails the build if a Phase
05 transcript slice loses its golden transcript or replay test file.

## Release Gates

- `Scripts/check-direct-mutation-callers.sh` blocks new direct-mutation
  paths unless they route through the runtime or carry an allowlist
  rationale in the script.
- `Scripts/check-kernel-abi-goldens.sh` verifies stable kernel ABI
  surfaces. Regenerate and verify goldens when touching
  `Sources/COmniWMKernels/` or `Zig/omniwm_kernels/src/`.
