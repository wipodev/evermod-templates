# 🧩 EverMod Templates

Official template profiles and code generation pipelines for the **EverMod Ecosystem**. This repository contains the Jinja2 blueprint configurations, Gradle wrappers, and metadata profiles used by the [EverMod CLI](https://evermod.wipodev.com) to automate multi-version Forge workspace creation.

---

## 🚀 Overview

`evermod-templates` powers the dynamic project creation process. Instead of static MDK files, it relies on a **Pipeline-Driven Generation Engine**.

When executing project creation commands in the CLI, this repository provides:

- **Modular Multi-Project Structure**: Pre-configured Gradle setup designed for single or multi-version Forge workspaces.
- **Jinja2 Dynamic Rendering**: Automated variable interpolation for package paths, Mod IDs, Java versions, and dependencies.
- **Profile Driven Engine**: Fully customizable orchestration defined via `templates.json`.
- **Unified Technical Profiles**: Technical metadata mapping for Minecraft versions ranging from `1.19.2` up to `1.21.x+`.

---

## 📦 Repository Structure

The layout is organized into functional zones to isolate root project settings from modular version projects:

```text
evermod-templates/
├── templates.json          # Master execution pipeline for CLI project generation
├── version.json            # Repository metadata and version tracking
├── version_profiles.json   # Deep configuration mapping per Minecraft/Forge version
├── root/                   # Base workspace files (Gradle wrapper, settings, root build)
│   ├── build.gradle
│   ├── gradlew / gradlew.bat
│   ├── gradle.properties.j2
│   └── settings.gradle.j2
├── src/                    # Java source templates and common resources
│   ├── MainMod.java.j2
│   ├── mods.toml
│   └── logo.png
└── projects/               # Version-specific project templates
    ├── build.gradle.j2
    ├── gradle.properties.j2
    └── pack.mcmeta.j2
```

---

## ⚙️ Architecture & Mechanics

### 1. The Pipeline Engine (`templates.json`)

The `templates.json` file dictates how the CLI constructs the workspace. Each profile defines a execution pipeline of file copies and Jinja2 renderings:

```json
{
  "standar": {
    "description": "Standard multi-version Forge workspace structure",
    "pipeline": [
      {
        "origin": "root/settings.gradle.j2",
        "target": "settings.gradle",
        "jinja": true,
        "loop_versions": false
      },
      {
        "origin": "projects/build.gradle.j2",
        "target": "projects/forge-{{minecraft_version}}/build.gradle",
        "jinja": true,
        "loop_versions": true
      }
    ]
  }
}
```

- `origin`: File path inside this template repository.

- `target`: Destination path in the target workspace (supports dynamic placeholders).

- `jinja`: If `true`, the CLI processes the file using the Jinja2 template engine.

- `loop_versions`: If `true`, the pipeline replicates and renders the file for every selected Minecraft version.

### 2. Technical Profiles (`version_profiles.json`)

Contains target properties required for exact Forge, Gradle, Java Toolchain, and dependency compatibility across Minecraft releases:

```json
{
  "1.20.1": {
    "minecraft_version_range": "[1.20.1,1.21)",
    "forge_version": "47.4.10",
    "java_version": "17",
    "remapping": true,
    "geckolib_version": "1.20.1:4.8.2",
    "pack_format": 15
  }
}
```

---

## 🛠️ CLI Integration Workflow

1. **Fetch / Sync**: The CLI syncs the template cache (`~/.evermod/templates`) with this repository.

2. **Profile Selection**: Reads `templates.json` to present available workspace profiles to the developer.

3. **Variable Mapping**: Prompts for mod metadata (ID, Name, Package, Target Minecraft Versions).

4. **Pipeline Execution**: The CLI processes each entry in `templates.json`, expanding templates like `MainMod.java.j2` and version subprojects into a ready-to-run environment.

---

## 🧠 About EverMod

**EverMod** is a modular framework and CLI ecosystem created by **wipodev** to streamline multi-version Minecraft Forge mod development. It allows developers to write core logic once and seamlessly compile across multiple Minecraft and Forge versions without manual mapping or Gradle boilerplate management.

- **Main Framework**: [EverMod](https://evermod.wipodev.com)
- **Command Line Interface**: [EverMod CLI](https://evermod.wipodev.com)

---

## ⚖️ License

Distributed under the terms of the **GNU Lesser General Public License v2.1**. See [root/LICENSE.txt](root/LICENSE.txt) for the full license text and terms regarding Forge MDK redistribution.

© 2026 **wipodev** — Created for the EverMod ecosystem.
