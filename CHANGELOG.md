# 🧾 EverMod Templates — Changelog

All notable changes to this project will be documented in this file.  
This file complements `manifest.json`, which always describes only the latest version.

---

## [1.1.0] - 2025-11-02

### Changed

- Unified all Forge build templates into a single dynamic Jinja2-based system.
- Replaced per-version `build.gradle` files with a single parameterized template for automatic generation.
- Updated `versions.json` structure to include expanded metadata (Java version, reobf, eventBus7, etc.).
- Improved CLI integration — templates are now fully version-aware and self-contained.

### Added

- Introduced `MainMod.java.j2` template with placeholders for `mod_id`, `mod_group`, and `mod_authors`.
- Added support for rendering `build.gradle`, `gradle.properties`, and main mod class using Jinja2.
- Included default mod structure templates: `mods.toml`, `pack.mcmeta`, `LICENSE.txt`, and Gradle wrapper files.
- Implemented automatic generation of complete mod projects from a single universal template.

### Removed

- Deprecated individual `build.gradle` templates for each Forge version in favor of the unified Jinja2 template system.

---

## [1.0.0] - 2025-10-30

### Added

- Initial release of EverMod Forge templates.
- Added base `gradle.properties.template` with EverMod placeholders.
- Included `build.gradle` templates for:
  - Forge 1.19.2
  - Forge 1.20.1
  - Forge 1.21
- Introduced `versions.json` for version mapping and CLI integration.
- Created `manifest.json` for update tracking.
