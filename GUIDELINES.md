# GalaxySol.CS — Development Guidelines 🛠️

This document defines the strict architectural rules, namespace standards, and commit conventions for the GalaxySol ecosystem. Follow these rules to keep the codebase clean and highly modular.

---

## 📂 Namespaces & Project Directory Standards

To prevent code clutter and keep IntelliSense clean, every module (project) must strictly follow three specific levels of visibility:

### 1. Root Namespace (`GalaxySol.[Layer].[Module]`)
* **Purpose:** Publicly exposed entry points.
* **What goes here:** The main service engines, configuration option schemas, and primary DTOs that the consumer needs immediately.
* **Rule:** A consumer should be able to access the core functionality with a single `using` statement.

### 2. Interfaces Namespace (`GalaxySol.[Layer].[Module].Interfaces`)
* **Purpose:** Code contracts and abstractions.
* **What goes here:** All public interfaces (`I...Service`, `I...Repository`).
* **Rule:** Keeps high-level abstractions isolated from direct implementation details.

### 3. Internal Namespace (`GalaxySol.[Layer].[Module].Internal` or `.SubServices`)
* **Purpose:** Encapsulated "under-the-hood" logic.
* **What goes here:** Minor sub-services, background workers, and private utility classes that are only required within the module itself.
* **Rule:** These classes should ideally be marked as `internal` to prevent leaking into the global code completion.

---

## 💾 Git Commit Convention (Conventional Commits)

Every commit must represent a single, compiled logical action. The solution must build successfully (`Ctrl + Shift + B`) before pushing any changes.

### Commit Message Format
```text
type(module): short description in lowercase
```

### Allowed Types:
* 🚀 **`feat`** — Adding new features, methods, or logic files (e.g., `feat(ffmpeg): FFmpegAudioService: implement mp3 extraction`).
* 🐛 **`fix`** — Bug fixes, compilation errors, or typo corrections (e.g., `fix(scaffolder): Pipeline: fix directory creation path`).
* 🧹 **`chore`** — Routine maintainence: project setup, `.slnx` file editing, or package updates (e.g., `chore(scaffolder): init project structure`).
* 📝 **`docs`** — Documentation updates, README changes, or markdown guides (e.g., `docs(readme): update project architecture guide`).
* 🎨 **`style`** — Code formatting, linting fixes, removing unused usings (does not affect logic).

---

## 📐 Project Isolation Rule
Each utility, helper, or service must be generated as a **standalone `.csproj` project**. This ensures that the .NET compiler can perfectly apply **code trimming** during assembly optimization, removing unused third-party NuGet dependencies.
