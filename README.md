# 🧩 EverMod Templates

**EverMod Templates** is the official repository of reusable Forge **MDK templates**  
used by the [EverMod CLI](https://github.com/wipodev/evermod-cli) to create  
and manage Minecraft Forge mods across multiple versions.

---

## 🧱 Purpose

This repository provides a set of **standardized Gradle build templates** and  
configuration files that allow the EverMod CLI to generate ready-to-build  
Forge mod projects with unified structure and naming conventions.

By maintaining all Forge-specific templates here, EverMod ensures:

- Consistent Gradle setup across all supported Minecraft versions.
- Faster mod creation via the `evermod create` command.
- Centralized updates and changelogs for version control.

---

## 🚀 How It Works

When you run:

```bash
evermod create MyMod 1.20.1
```

The CLI automatically:

1. Reads `versions.json` from your global EverMod directory (`~/.evermod/templatesMDK`).
2. Selects the proper `build.gradle` template for the specified version.
3. Copies the `gradle.properties.template` file and replaces all placeholders:
   ```
   [mcv] → Minecraft version
   [fv]  → Forge version
   [fm]  → Forge major version
   [mid] → Mod ID
   [systemProp] → Version-specific Forge Gradle system properties
   ```
4. Registers the new mod automatically in your workspace `settings.gradle` file.

---

## 📦 Repository Structure

```
evermod-templates/
│
├── manifest.json                # Version metadata and changelog
│
└── templatesMDK/
    ├── gradle.properties.template
    ├── build_1.19.2.gradle
    ├── build_1.20.1.gradle
    ├── build_1.21.gradle
    └── versions.json
```

### `manifest.json`

Describes the latest version of the templates, changelog, and release metadata.  
This file is read directly by `evermod update` to detect new versions.

### `versions.json`

Maps Minecraft versions to Forge Gradle templates.  
Used by the `evermod create` command to select the correct build file.

---

## 🔄 Updating Templates

To update the templates locally, simply run:

```bash
evermod update
```

The CLI will:

1. Read `manifest.json` directly from this repository.
2. Compare it to your local version (`~/.evermod/version.json`).
3. Show you the changelog.
4. Ask if you want to update.
5. Clone this repository and replace your local templates.

---

## 🧠 About EverMod

**EverMod** is a modular framework and CLI designed by **Wipodev**  
to simplify multi-version Minecraft Forge mod development.  
It allows mods to share a single codebase and compile for different Forge versions  
without changing imports or project structure.

👉 Main CLI: [EverMod Framework](https://github.com/wipodev/EverMod)

---

## ⚖️ License

© 2025 Wipodev — All rights reserved.  
The EverMod templates are intended for internal and personal use  
within the EverMod development ecosystem.
