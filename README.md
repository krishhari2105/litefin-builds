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
| **Litefin-fork** | `krishhari2105/litefin` | `litefin-emby-compatiblity` | `*.wgt`, `*.ipk` (Modern) |
| **Moonfin** | `Moonfin-Client/Smart-TV` | `main` | `*.wgt`, `*.ipk` |

## How to Trigger a Build

### Automatic Trigger (Litefin-fork)
The `Litefin-fork` workflow automatically triggers when changes are pushed to your fork repository:
- **Immediate Push Dispatch**: Automatically dispatches a build whenever commits are pushed to `litefin-emby-compatiblity` in `krishhari2105/litefin` (via GitHub Actions `repository_dispatch`).
- **Periodic Check (Zero-PAT)**: Runs a scheduled commit check every 30 minutes. If new commits are detected on `litefin-emby-compatiblity`, it automatically triggers a build.
- **Single Rolling Release**: When a new fork build succeeds, older `litefin-fork` releases and tags are automatically deleted and replaced with the new build so releases never stack up.

### Manual Trigger
1. Navigate to the **Actions** tab in this repository.
2. Select the workflow you wish to run:
   - `Litefin-dev Build & Release` for upstream dev branch
   - `Litefin-release Build & Release` for upstream stable release branch
   - `Litefin-fork Build & Release` for your fork (`litefin-emby-compatiblity` by default)
3. Click **Run workflow**, optionally specify or change the branch name, and click **Run workflow**.
4. Once completed, download the `.wgt` and `.ipk` packages directly from the newly created release under the **Releases** tab.
