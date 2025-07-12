# Zephyr Container Images

> Forked from [embeddedcontainers/zephyr](https://github.com/embeddedcontainers/zephyr)

Develop Zephyr applications using OCI-compatible Docker images.

Currently there are two types of images - a "base" image that contains the core dependencies to build a Zephyr application for a target SDK version and ones for a specific target architecture. Most users will generally interact with the architecture-specific images.

# Getting container images

## Build images locally

Building images locally ensures you can trust the source of the image, as well as allow you to modify the container image configuration.

### Building with Docker CLI

_Build the base image_

```
docker build \
  --build-arg ZEPHYR_SDK_VERSION=0.17.2 \
  -f "./zephyr-base/Dockerfile" \
  -t zephyr:base-0.17.2SDK \
  "./zephyr-base"
```

_To build an image for Arm Cortex-M targets:_


```
docker build \
  --build-arg ZEPHYR_SDK_VERSION=0.17.2 \
  --build-arg ZEPHYR_SDK_TOOLCHAINS="-t arm-zephyr-eabi" \
  -f "./zephyr-arch/Dockerfile" \
  -t zephyr:arm-0.17.2SDK \
  "./zephyr-arch"
```

_To build an image for multiple toolchains:_

```
docker build \
  --build-arg ZEPHYR_SDK_VERSION=0.17.2 \
  --build-arg ZEPHYR_SDK_TOOLCHAINS="-t arm-zephyr-eabi -t riscv64-zephyr-elf" \
  -f "./zephyr-arch/Dockerfile" \
  -t zephyr:arm_riscv-0.17.2SDK \
  "./zephyr-arch"
```

_There is a different Dockerfile for Posix target like `native_sim`. To build:_

```
docker build \
  --build-arg ZEPHYR_SDK_VERSION=0.17.2 \
  -f "./zephyr-posix/Dockerfile" \
  -t zephyr:posix-0.17.2SDK \
  "./zephyr-posix"
```

## Zephyr SDK Version

[Zephyr SDK Version Compatibility Matrix](https://github.com/zephyrproject-rtos/sdk-ng/wiki/Zephyr-SDK-Version-Compatibility-Matrix)
