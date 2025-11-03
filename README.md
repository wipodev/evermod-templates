# 🧩 EverMod Templates

**EverMod Templates** is the official repository of reusable **Forge MDK templates**
used by the [EverMod CLI](https://github.com/wipodev/evermod-cli) to create and manage
Minecraft Forge mods across multiple versions — **from 1.19.2 up to the latest releases.**

---

## 🧱 Purpose

This repository provides a **unified, dynamic, and version-aware** system
for generating Forge mod projects using **Jinja2 templates**.

Each mod created with the EverMod CLI uses these templates to build
a fully configured project — complete with Gradle files, mod metadata,
and starter Java classes — all tailored to the selected Minecraft version.

By maintaining all logic and version configuration here, EverMod ensures:

- ✅ Consistent project structure across all Minecraft versions.
- ⚡ Fast mod creation via the interactive `evermod create` command.
- 🔄 Centralized updates for Gradle and Forge version compatibility.
- 🧩 Automatic registration in multi-mod workspaces.

---

## 🚀 How It Works

When you run:

```bash
evermod create
```

The CLI starts an **interactive wizard** that:

1. Asks for basic information (mod name, mod ID, author, Minecraft version, etc.).
2. Reads the configuration for that version from `versions.json`.
3. Uses the **Jinja2 templates** to render:

   - `build.gradle`
   - `gradle.properties`
   - `MainMod.java` (auto-configured main mod class)

4. Copies the base folder structure:

   ```
   src/main/java/net/{mod_group}/{mod_id}/
   src/main/resources/
   src/main/resources/META-INF/
   ```

5. Inserts `mods.toml`, `pack.mcmeta`, and `LICENSE.txt` automatically.
6. If not part of a workspace, it also includes the Gradle wrapper and `.gitignore` files.
7. Registers the new mod inside your workspace `settings.gradle` when applicable.

---

## 📦 Repository Structure

```
evermod-templates/
├── CHANGELOG.md
├── manifest.json                # Template version info and changelog
├── README.md
└── templates/
    ├── gradle/wrapper/           # Wrapper configuration files
    ├── .gitattributes
    ├── .gitignore
    ├── build.gradle.j2           # Jinja2 template for all Forge builds
    ├── gradle.properties.j2      # Jinja2 template for properties
    ├── gradlew                   # Gradle wrapper scripts
    ├── gradlew.bat               # Gradle wrapper scripts
    ├── LICENSE.txt               # Forge license
    ├── MainMod.java.j2           # Template for the mod's main class
    ├── mods.toml                 # Standard Forge mod metadata file
    ├── pack.mcmeta               # Required by Minecraft for resource packs
    ├── settings.gradle           # Default Gradle settings file for standalone mods
    └── versions.json             # Version mapping and rendering metadata
```

### 🗂️ Description by File

| File                               | Purpose                                                          |
| ---------------------------------- | ---------------------------------------------------------------- |
| **CHANGELOG.md**                   | Contains version history in Markdown format.                     |
| **manifest.json**                  | Stores the latest release info and changelog for updates.        |
| **README.md**                      | Documentation about usage and structure.                         |
| **gradle/wrapper/**                | Holds the Gradle wrapper binaries and configuration.             |
| **.gitattributes**, **.gitignore** | Git configuration for line endings and ignored files.            |
| **build.gradle.j2**                | Jinja2 template for generating the mod's build file dynamically. |
| **gradle.properties.j2**           | Template defining mod metadata and Gradle configuration.         |
| **gradlew**, **gradlew.bat**       | Gradle launcher scripts for Linux/macOS and Windows.             |
| **LICENSE.txt**                    | Default Forge license template.                                  |
| **MainMod.java.j2**                | Starter Java file for the mod’s entry point.                     |
| **mods.toml**, **pack.mcmeta**     | Required Forge and Minecraft metadata.                           |
| **settings.gradle**                | Basic settings for mods created outside a workspace.             |
| **versions.json**                  | Defines version-specific properties for Minecraft and Forge.     |

---

## ⚙️ `versions.json`

This file defines every supported Minecraft–Forge version combination,
along with their build metadata and Gradle configuration:

```json
{
  "1.21.10": {
    "forge_version": "60.0.14",
    "forge_gradle": "[6.0.36,6.2)",
    "java_version": "21",
    "reobf": false,
    "include_maven_repositories": true,
    "eventBus7": true,
    "eventBus_version": "7.0-beta.12",
    "merge_source_sets": true
  }
}
```

Each entry drives the automatic generation of the final `build.gradle`
and `gradle.properties` through the Jinja2 rendering process.

---

## 🔄 Updating Templates

To update your local templates, run:

```bash
evermod update
```

The CLI will:

1. Fetch the latest release info from this repository (`manifest.json`).
2. Compare it with your local version (`~/.evermod/version.json`).
3. Show you the changelog.
4. Download and replace your local template set automatically.

---

## 🧠 About EverMod

**EverMod** is a modular framework and CLI by **Wipodev**
designed to simplify **multi-version Minecraft Forge mod development**.
It enables developers to maintain a single, clean codebase that can
compile across different Forge versions without manually adjusting mappings
or Gradle configurations.

👉 Main Project: [EverMod Framework](https://github.com/wipodev/EverMod)

---

## ⚖️ License

© 2025 **Wipodev** — All rights reserved.
The EverMod templates are intended for internal and personal use
within the EverMod ecosystem. Redistribution outside of EverMod
must retain credit to the author and repository source.
