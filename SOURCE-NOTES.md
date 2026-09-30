# SOURCE-NOTES.md

This snapshot publishes the **text/source files** of NOVA v9.13.2 (source tree at
head `b2af40b38706f624c823d85d9d0ec7efa49711c2`). Binary artifacts, backup/cruft
files, one oversized dataset file, and anything that failed the pre-push secret
scan were intentionally left out. They are listed below so the snapshot is
auditable.

- Source files published: **126** (plus this `SOURCE-NOTES.md`)
- Binary artifacts excluded: **8**
- Cruft / backup files excluded: **42**
- Oversized files excluded: **1**
- Secret-scan skips: **0**

## Why binaries are excluded

The binaries below are not needed to read or review the source. The prebuilt
inference-engine AAR (`llama-release.aar`) can be rebuilt from the engine build
patches kept under `tmp/`; the embedding model (all-MiniLM-L6-v2 ONNX) is fetched
and sha256-verified by CI at build time rather than stored here; fonts, native
`.so` libraries, the Gradle wrapper jar and the release keystore are toolchain or
build artifacts. The keystore is a signing secret and is never published.

## Excluded binaries

| Path | Size | Blob SHA |
| --- | ---: | --- |
| `android/app/libs/llama-release.aar` | 18.0 MB | `10415bef8fb6cf608b635f48ac8342af9dadd365` |
| `android/app/src/main/res/font/inter_bold.ttf` | 410.6 KB | `9fb9b751e5b2441054f6eef670da7b3f53a3505a` |
| `android/app/src/main/res/font/inter_medium.ttf` | 407.5 KB | `458cd0601d28013d3817481aa2839c9bbb5ded70` |
| `android/app/src/main/res/font/inter_regular.ttf` | 402.0 KB | `b7aaca8de1fe458399e17311d35d543a1fa2f984` |
| `android/app/src/main/res/font/inter_semibold.ttf` | 409.9 KB | `47f8ab1d68144fc004b310d65d95180d502b449b` |
| `android/gradle/wrapper/gradle-wrapper.jar` | 46.4 KB | `eddabd2eef8d94a5437d6168ff9c87a78ff725b3` |
| `android/nova-release-v2.keystore` | 1.1 KB | `15eb75c304b4dc00daf2f8300e0aed4be6384894` |
| `nova-test/jni/arm64-v8a/libai-chat.so` | 66.0 KB | `21f9c832bec8f389dc9fc5820b29a99cf52c6742` |

## Excluded cruft / backup files

These are working-copy backups, `before_` snapshots, Kivy `.kv` drafts, and
root-level pasted debug logs — not part of the current source.

| Path | Reason | Size |
| --- | --- | ---: |
| `inference.txt` | root-txt-dump | 18.3 KB |
| `init.txt` | root-txt-dump | 9.1 KB |
| `loadmodel.txt` | root-txt-dump | 14.7 KB |
| `main_backup.py` | backup | 5.4 KB |
| `main_before_keyboard_fix.kv` | before_ | 973 B |
| `main_before_keyboard_fix.py` | before_ | 4.2 KB |
| `nova_128_backup.py` | backup | 4.2 KB |
| `nova_4096_backup.py` | backup | 4.2 KB |
| `nova_backup.py` | backup | 4.2 KB |
| `nova_before_11chat.py` | before_ | 4.3 KB |
| `nova_before_20chat.py` | before_ | 4.2 KB |
| `nova_before_calculator.py` | before_ | 3.4 KB |
| `nova_before_chat_history.py` | before_ | 4.2 KB |
| `nova_before_clean_final.py` | before_ | 4.4 KB |
| `nova_before_clean_history.py` | before_ | 3.2 KB |
| `nova_before_clean_output.py` | before_ | 4.2 KB |
| `nova_before_cleanup.py` | before_ | 3.3 KB |
| `nova_before_file_fix.py` | before_ | 4.2 KB |
| `nova_before_final_llama_fix.py` | before_ | 4.2 KB |
| `nova_before_final_output_fix.py` | before_ | 4.2 KB |
| `nova_before_history_fix.py` | before_ | 2.9 KB |
| `nova_before_history_v2.py` | before_ | 3.0 KB |
| `nova_before_lib_fix.py` | before_ | 4.2 KB |
| `nova_before_output_fix.py` | before_ | 4.2 KB |
| `nova_before_output_parser.py` | before_ | 4.2 KB |
| `nova_before_persistent_11chat.py` | before_ | 4.5 KB |
| `nova_before_persistent_final.py` | before_ | 4.5 KB |
| `nova_before_persistent_model.py` | before_ | 4.4 KB |
| `nova_before_server.py` | before_ | 4.6 KB |
| `nova_before_short_answers.py` | before_ | 3.0 KB |
| `nova_before_silent_fix.py` | before_ | 4.4 KB |
| `nova_before_silent_output.py` | before_ | 4.2 KB |
| `nova_before_simple_history.py` | before_ | 3.5 KB |
| `nova_before_simpleio_final.py` | before_ | 4.2 KB |
| `nova_clean_4096_backup.py` | backup | 4.2 KB |
| `nova_file_output_backup.py` | backup | 4.2 KB |
| `nova_llama_output.txt` | root-txt-dump | 1.2 KB |
| `nova_log.txt` | root-txt-dump | 20.7 KB |
| `nova_simpleio_backup.py` | backup | 4.4 KB |
| `nova_stuck_backup.py` | backup | 4.2 KB |
| `nova_test.txt` | root-txt-dump | 0 B |
| `rebuild.txt` | root-txt-dump | 29 B |

## Excluded oversized files

| Path | Size | Blob SHA | Reason |
| --- | ---: | --- | --- |
| `wiki/articles-v1.txt` | 6.8 MB | `9a8de46e8856e560bf97ca2425c56bdb39d14430` | exceeds the commit API payload limit (HTTP 413) |

This large wiki dataset is a text file, but its size exceeds the commit API's
request limit, so it could not be included in this automated snapshot. It can be
added manually if desired.

## Secret-scan skips

None. No published file matched the pre-push secret patterns
(`ghp_`, `github_pat_`, `sk-`, `AKIA`, `PRIVATE KEY`, `api_key=`, `password=`),
and no `.env` or keystore file was published.

