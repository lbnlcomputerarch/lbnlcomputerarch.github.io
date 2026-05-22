---
layout: page
title: Adding Tools to Your Environment
nav_order: 4
permalink: /docs/adding-tools/
parent: Documentation
---

## Adding Tools to Your Environment

This guide covers installing and managing software tools on CAG computing resources. On all CAG servers, you can find the tools in `/tools`.

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

## AMD/Xilinx Tools

### See Available Versions

```bash
source /tools/source-vitis.sh --list
```

#### Example

```bash
❯ source /tools/source-vitis.sh --list
Available Vitis versions in /tools:
-----------------------------------
AMD (2025 and newer):
  - 2025.1
  - 2025.1.1
  - 2025.2
  - 2025.2.1
Xilinx (Pre-2025):
  - 2022.1
  - 2022.2
  - 2023.1
```

### Load the tool version

```bash
source /tools/source-vitis.sh VERSION
```

#### Example

```bash
source /tools/source-vitis.sh 2025.1
```

## ModelSim SE 2021.1

### Load the tool

```bash
source /tools/source-modelsimse-2021.1.sh
```
