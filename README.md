# litefin-builds

Automated GitHub Actions CI/CD workflows for building modern **Litefin** packages for Samsung Tizen and LG webOS smart TVs.

## Overview

This repository builds **Modern (ES6+)** packages for Litefin without wasting CI runner time or memory on older legacy/ultra-legacy transpilations:
- **Samsung Tizen**: `Litefin-<version>-Tizen-Modern.wgt` (Tizen 6.5+ / 2022+ TVs)
- **LG webOS**: `Litefin-<version>-webOS-Modern.ipk` (webOS 6.0+ / 2021+ TVs)

By using `npm run package:modern` (`gulp buildPackageCombinedModern`), only the modern Webpack target is compiled and packaged, avoiding Babel ES5 transpilation, Terser overhead, and legacy polyfill bundles.

## Available Workflows

| Workflow | Source Repository | Default Branch | Artifacts |
| :--- | :--- | :--- | :--- |
| **Litefin-dev** | `moazsalem/litefin` | `development` | `*.wgt`, `*.ipk` (Modern) |
| **Litefin-release** | `moazsalem/litefin` | `release` | `*.wgt`, `*.ipk` (Modern) |
| **Litefin-fork** | `krishhari2105/litefin` | `development` | `*.wgt`, `*.ipk` (Modern) |
| **Moonfin** | `Moonfin-Client/Smart-TV` | `main` | `*.wgt`, `*.ipk` |

## How to Trigger a Build

1. Navigate to the **Actions** tab in this repository.
2. Select the workflow you wish to run:
   - `Litefin-dev Build & Release` for upstream dev branch
   - `Litefin-release Build & Release` for upstream stable release branch
   - `Litefin-fork Build & Release` for your fork
3. Click **Run workflow**, optionally specify or change the branch name, and click **Run workflow**.
4. Once completed, download the `.wgt` and `.ipk` packages directly from the newly created release under the **Releases** tab.
