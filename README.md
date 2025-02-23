# setup-zephyr

This actions initializes a Zephyr based project, downloading the Zephyr SDK and
the necessary modules for a West based [Zephyr workspace application][1].

# Basic usage

```yaml
- name: Setup Zephyr project
  uses: <TODO>/zephyr-setup@v1
  with:
    toolchains: arm-zephyr-eabi
```

# Scenarios

## Application and west.yml in an "app" subdirectory

```yaml
- name: Checkout
  uses: actions/checkout@v3

- name: Setup Zephyr project
  uses: <TODO>/zephyr-setup@v1
  with:
    toolchains: arm-zephyr-eabi

- name: Build
  run: |
    west build app
```

## Application and west.yml at the root of the repository

```yaml
- name: Checkout
  uses: actions/checkout@v3
  with:
    path: app

- name: Setup Zephyr project
  uses: <TODO>/zephyr-setup@v1
  with:
    toolchains: arm-zephyr-eabi

- name: Build
  run: |
    west build app
```

## Use a specific SDK version and multiple compilers

```yaml
- name: Setup Zephyr project
  uses: <TODO>/zephyr-setup@v1
  with:
    toolchains: arm-zephyr-eabi:riscv64-zephyr-elf
    sdk-version: 0.16.3
```

## Use a specific Zephyr version

```yaml
- name: Setup Zephyr project
  uses: <TODO>/zephyr-setup@v1
  with:
    toolchains: arm-zephyr-eabi:riscv64-zephyr-elf
    sdk-version: 0.16.3
    zephyr-version: v3.5.0
```
## Execute west init with custom project manifest file

If you set opetion ```manifest-file:``` - ```zephyr-version``` wiil be ignored and init env from parametrs from manifest file.

```yaml
- name: Setup Zephyr project
  uses: <TODO>/zephyr-setup@v1
  with:
    toolchains: arm-zephyr-eabi:riscv64-zephyr-elf
    sdk-version: 0.16.3
    manifest-file: <path to file in project>
    zephyr-version: v3.5.0
```


[1]: https://docs.zephyrproject.org/latest/develop/application/index.html#zephyr-workspace-app

