# setup-zephyr

This GitHub Action initializes a Zephyr-based project, downloading the Zephyr SDK and the necessary modules for a West-based [Zephyr workspace application][1].

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `zephyr-version` | Zephyr version to use | No | `main` |
| `app-path` | Application code path, should contain a west.yml file | Yes | - |
| `manifest-file` | Manifest file for west init | No | - |
| `sdk-version` | Zephyr SDK version to use | No | `0.16.4` |
| `sdk-base` | Base URL of the Zephyr SDK | No | `https://github.com/zephyrproject-rtos/sdk-ng/releases/download` |
| `toolchains` | List of toolchains to install, colon separated | No | `arm-zephyr-eabi:riscv64-zephyr-elf` |

## Basic Usage

```yaml
- name: Setup Zephyr project
  uses: <TODO>/setup-zephyr@v1
  with:
    app-path: app
    toolchains: arm-zephyr-eabi
```

## Scenarios

### Application and west.yml in an "app" subdirectory

```yaml
- name: Checkout
  uses: actions/checkout@v4

- name: Setup Zephyr project
  uses: <TODO>/setup-zephyr@v1
  with:
    app-path: app
    toolchains: arm-zephyr-eabi

- name: Build
  run: |
    west build app
```

### Application and west.yml at the root of the repository

```yaml
- name: Checkout
  uses: actions/checkout@v4
  with:
    path: app

- name: Setup Zephyr project
  uses: <TODO>/setup-zephyr@v1
  with:
    app-path: app
    toolchains: arm-zephyr-eabi

- name: Build
  run: |
    west build app
```

### Use a specific SDK version and multiple toolchains

```yaml
- name: Setup Zephyr project
  uses: <TODO>/setup-zephyr@v1
  with:
    app-path: app
    toolchains: arm-zephyr-eabi:riscv64-zephyr-elf
    sdk-version: 0.16.3
```

### Use a specific Zephyr version

```yaml
- name: Setup Zephyr project
  uses: <TODO>/setup-zephyr@v1
  with:
    app-path: app
    toolchains: arm-zephyr-eabi:riscv64-zephyr-elf
    sdk-version: 0.16.3
    zephyr-version: v3.5.0
```

### Execute west init with custom project manifest file

If you set the `manifest-file` option, the `zephyr-version` will be ignored and the environment will be initialized from parameters in the manifest file.

```yaml
- name: Setup Zephyr project
  uses: <TODO>/setup-zephyr@v1
  with:
    app-path: app
    toolchains: arm-zephyr-eabi:riscv64-zephyr-elf
    sdk-version: 0.16.3
    manifest-file: west.yml
```

## Platform Support

This action supports the following platforms:
- Linux (x64, ARM64)
- macOS (x64, ARM64)
- Windows (x64)

## Features

- **Caching**: Automatically caches the Zephyr SDK and Python packages for faster subsequent runs
- **Cross-platform**: Works on Linux, macOS, and Windows runners
- **Flexible toolchain selection**: Install only the toolchains you need
- **Custom manifest support**: Use your own west.yml manifest file
- **Version pinning**: Pin specific versions of Zephyr and the SDK for reproducible builds

## Available Toolchains

Common toolchains available for installation:
- `arm-zephyr-eabi` - ARM Cortex-M and Cortex-A
- `riscv64-zephyr-elf` - RISC-V 64-bit
- `x86_64-zephyr-elf` - x86 64-bit
- `xtensa-espressif_esp32_zephyr-elf` - ESP32
- `xtensa-espressif_esp32s2_zephyr-elf` - ESP32-S2
- `xtensa-espressif_esp32s3_zephyr-elf` - ESP32-S3

Multiple toolchains can be specified using colon separation: `arm-zephyr-eabi:riscv64-zephyr-elf`

[1]: https://docs.zephyrproject.org/latest/develop/application/index.html#zephyr-workspace-app

