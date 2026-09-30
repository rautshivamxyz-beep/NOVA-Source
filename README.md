# NOVA — a fully offline, private AI assistant for Android

NOVA is a fully offline AI assistant for Android. It runs Llama-family language
models **directly on the phone** through `llama.cpp` (via the official Android
binding), so conversations, retrieval and reasoning all happen on-device — no
cloud service is required for the assistant to work.

This repository is a **clean source snapshot** of the latest NOVA version
(v9.13.2). It contains the source tree only — no commit history, no release
binaries, no private assets. See `SOURCE-NOTES.md` for exactly what was left
out and why.

## What it does

- **Local LLM inference** — runs GGUF models on-device with `llama.cpp`; no
  network round-trip is needed to generate a response.
- **On-device embedding-based retrieval** — a small sentence-embedding model
  (all-MiniLM-L6-v2, ONNX) powers local semantic search / memory over the
  user's own notes and documents.
- **Tutor mode** — a guided, step-by-step teaching mode for explanations and
  practice.
- **Notification awareness** — NOVA can read and reason over the user's
  notifications to stay contextually useful.
- **Backup and restore** — export and import app data locally.
- **Delta updates** — incremental patch-style updates rather than full
  re-downloads.

## Design principles

- **Local-first** — everything the assistant does runs on the device; there is
  no server-side component.
- **Ask-first networking** — the app does not reach the network on its own; any
  outbound request is initiated with the user's knowledge.
- **No accounts** — there is no sign-in, no user profile and no server-side
  identity.
- **No autopilot** — the assistant does not take actions by itself.
- **Human confirms every action** — any state-changing action is surfaced to the
  user for explicit confirmation before it happens.

## Build notes

NOVA is an Android application built with Gradle.

- Build with the standard Android Gradle toolchain from the `android/`
  directory.
- **Embedder model (CI):** the continuous-integration build downloads the
  all-MiniLM-L6-v2 ONNX embedder from a pinned URL and verifies its **sha256**
  before use, so the model is fetched at build time rather than vendored.
- **Inference engine:** the prebuilt inference engine AAR
  (`android/app/libs/llama-release.aar`, the `com.arm.aichat` binding) is **not
  included in this snapshot** — see `SOURCE-NOTES.md`. The engine is rebuildable
  from the build patches kept under `tmp/`.
- **Engine build patches:** the scripts that patch and rebuild the inference
  engine live in `tmp/`.
- GitHub Actions workflows for building, delta updates, engine spec updates and
  the wiki dataset are under `.github/workflows/`.

## License

Source is published for reference and learning. No license is granted for reuse
or redistribution unless a LICENSE file is added.
