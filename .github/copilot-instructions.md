Purpose

This repository is a collection of APRS-format and device-format documents used by OGN (Open Glider Network). It contains specifications, example messages and device/vendor format notes (text/PDF). It is primarily reference material rather than an application repository.

Quick commands

- Build / test / lint: none in this repository (no local source project found).
- Parser used by OGN (external): python-ogn-client (PyPI: ogn-client).
  - Install: pip3 install ogn-client
  - To inspect or run tests related to parsing, use the python-ogn-client repository and its pytest commands (e.g., pytest path/to/test::test_name).

High-level architecture (big picture)

- Role: canonical repository of APRS message formats, vendor/device format notes, and example message payloads used by OGN.
- Primary artifact types:
  - Human-readable format/spec documents (TXT, MD, PDF).
  - Example messages (aprsmsgs.txt, valid_messages).
  - aprsspec/ directory (APRS protocol text resources).
- How these are used in practice:
  - Consumers (parsers, validators, test suites) should treat these files as reference inputs.
  - Production parsing/clients live in separate code repos (see README.md: https://github.com/glidernet/python-ogn-client).

Key repository conventions and patterns

- File naming: device/vendor names and APRS appear in filenames (e.g., Naviter_APRS_format.md, FANET.protocol.txt). When adding new formats, follow the same pattern: <Vendor>_APRS_format.<md|txt|pdf>.
- Examples vs. specs: keep message examples in aprsmsgs.txt and valid_messages. Examples should be added as new lines/files rather than editing historical examples when demonstrating new encodings.
- Text-first canonical source: prefer the plain-text files (TXT/MD) as the authoritative source; PDFs are supporting artifacts.
- Encoding: files are plain UTF-8 text unless a format explicitly requires otherwise.
- Cross-references: add minimal README updates (or a new short index file) when adding new vendor docs so consumers can discover them.

Guidance for Copilot sessions working on this repo

1. Start by reading README.md and aprsspec/, then search valid_messages and aprsmsgs.txt for concrete examples.
2. If work involves parsing/validation, reference or delegate to python-ogn-client rather than inventing a new parser in this repo. Link to its tests and examples.
3. Searching: prefer ripgrep/rg (or the repo search tools) for patterns like "APRS", vendor names (Naviter, FANET, SPOT), or message keys found in aprsmsgs.txt.
   - Example search: rg -n "APRS|FANET|Naviter" --glob "**/*.{txt,md,PDF,pdf}"
4. When proposing format changes or additions:
   - Add a new file following existing naming conventions.
   - Add example messages to valid_messages or aprsmsgs.txt (new file or appended section) and reference them from README or a short index.
   - Do not remove or alter historical examples—append new examples and mark their provenance.
5. When asked to create code or tests that consume these specs, include unit tests that load examples from valid_messages/aprsmsgs.txt (so tests are deterministic and traceable back to a file in this repo).
6. Keep edits minimal and surgical: this repo is used as a canonical reference by other projects; preserve historical context.

Important files to check first

- README.md
- aprsmsgs.txt
- aprsspec/ (APRS spec resources)
- valid_messages
- Files with vendor/device names: Naviter_APRS_format.md, FANET.protocol.txt, SPOT API.txt, Skylines API.txt, etc.

Incorporated docs

- README.md: points users to python-ogn-client on GitHub and PyPI; keep this pointer up to date when adding or modifying parsing-related notes.

What this file is not

- This is not a contribution guide or coding style guide; it focuses on discovery, key repo patterns, and how Copilot should prioritize files and external parsers.

If updates are needed

- Add or update the small list under "Important files" and any repo-specific search hints.
- When adding vendor specs, add README links so Copilot can point developers to the right file quickly.
