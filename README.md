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
| **Litefin-fork** | `krishhari2105/litefin` | Chosen manually | `*.wgt`, `*.ipk` (Modern) |
| **Moonfin** | `Moonfin-Client/Smart-TV` | `main` | `*.wgt`, `*.ipk` |

## How to Trigger a Build

### Automatic Trigger (Litefin-dev)

The `Litefin-dev` workflow checks `moazsalem/litefin`'s `development` branch every 30 minutes. When it detects a commit that has not already been released, it builds the modern packages and updates the rolling `litefin-build-development` release.

GitHub Actions in this repository cannot directly subscribe to push events in the separate upstream repository, so polling provides automatic builds without requiring a token or workflow change in the upstream project. Each branch uses one rolling release tag; a successful rebuild replaces that release's previous `.wgt` and `.ipk` assets rather than creating additional releases.

### Manual Trigger

1. Navigate to the **Actions** tab in this repository.
2. Select the workflow you wish to run:
   - `Litefin-dev Build & Release` for an upstream Litefin branch
   - `Litefin-release Build & Release` for an upstream stable release branch
   - `Litefin-fork Build & Release` for a branch in `krishhari2105/litefin`
3. Click **Run workflow**, enter the branch name where required, and click **Run workflow**.
4. Once completed, download the `.wgt` and `.ipk` packages from the corresponding release under the **Releases** tab.

Re-running `Litefin-dev` or `Litefin-fork` for the same branch updates that branch's existing rolling release and replaces its package assets.
