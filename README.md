[![Docker Build](https://github.com/ai-dock/comfyui/actions/workflows/docker-build.yml/badge.svg)](https://github.com/ai-dock/comfyui/actions/workflows/docker-build.yml)

# AI-Dock + ComfyUI Docker Image

# Overview
# --------
# This Docker image allows you to run ComfyUI in a highly-configurable, cloud-first AI-Dock container.
# ComfyUI is a popular user interface for AI models, and this image makes it easy to deploy and manage.

# What is ComfyUI?
# ----------------
# ComfyUI is a user-friendly interface for interacting with AI models. It provides a simple and intuitive way to manage and deploy AI models.

Run [ComfyUI](https://github.com/comfyanonymous/ComfyUI) in a highly-configurable, cloud-first AI-Dock container.

> [!NOTE]
> These images do not bundle models or third-party configurations. You should use a [provisioning script](https://github.com/ai-dock/base-image/wiki/4.0-Running-the-Image#provisioning-script) to automatically configure your container. You can find examples, including `SD3` & `FLUX.1` setup, in `config/provisioning`.

## Documentation

# Introduction
# ------------
# All AI-Dock containers share a common base which is designed to make running on cloud services such as [vast.ai](https://link.ai-dock.org/vast.ai) as straightforward and user friendly as possible.

# What is AI-Dock?
# ----------------
# AI-Dock is a cloud-first containerization platform for AI models. It provides a simple and intuitive way to deploy and manage AI models in the cloud.

All AI-Dock containers share a common base which is designed to make running on cloud services such as [vast.ai](https://link.ai-dock.org/vast.ai) as straightforward and user friendly as possible.

#### Version Tags

# Versioning
# ----------
# The `:latest` tag points to `:latest-cuda` and will relate to a stable and tested version. There may be more recent builds

# What are version tags?
# ----------------------
# Version tags are used to identify different versions of the AI-Dock image. They can be used to specify a specific version of the image to use.

The `:latest` tag points to `:latest-cuda` and will relate to a stable and tested version. There may be more recent builds

Tags follow these patterns:

##### _CUDA_
- `:cuda-[x.x.x-base|runtime]-[ubuntu-version]`

##### _ROCm_
- `:rocm-[x.x.x-runtime]-[ubuntu-version]`

##### _CPU_
- `:cpu-[ubuntu-version]`

# Image Variants
# --------------
# Browse [ghcr.io](https://github.com/ai-dock/comfyui/pkgs/container/comfyui) for an image suitable for your target environment. Alternatively, view a select range of [CUDA](https://hub.docker.com/r/aidockorg/comfyui-cuda) and [ROCm](https://hub.docker.com/r/aidockorg/comfyui-rocm) builds at DockerHub.

# What are image variants?
# ------------------------
# Image variants are different versions of the AI-Dock image that are optimized for specific environments or use cases.

Browse [ghcr.io](https://github.com/ai-dock/comfyui/pkgs/container/comfyui) for an image suitable for your target environment. Alternatively, view a select range of [CUDA](https://hub.docker.com/r/aidockorg/comfyui-cuda) and [ROCm](https://hub.docker.com/r/aidockorg/comfyui-rocm) builds at DockerHub.

Supported Platforms: `NVIDIA CUDA`, `AMD ROCm`, `CPU`

## Additional Environment Variables

# Environment Variables
# ---------------------
# The following environment variables can be used to customize the behavior of the container.

# What are environment variables?
# -----------------------------
# Environment variables are used to customize the behavior of the container. They can be used to specify settings or options that affect how the container runs.

| Variable                 | Description |
| ------------------------ | ----------- |
| `AUTO_UPDATE`            | Update ComfyUI on startup (default `false`) |
| `CIVITAI_TOKEN`          | Authenticate download requests from Civitai - Required for gated models |
| `COMFYUI_ARGS`           | Startup arguments. eg. `--gpu-only --highvram` |
| `COMFYUI_PORT_HOST`      | ComfyUI interface port (default `8188`) |
| `COMFYUI_REF`            | Git reference for auto update. Accepts branch, tag or commit hash. Default: latest release |
| `COMFYUI_URL`            | Override `$DIRECT_ADDRESS:port` with URL for ComfyUI |
| `HF_TOKEN`               | Authenticate download requests from HuggingFace - Required for gated models (SD3, FLUX, etc.) |

See the base environment variables [here](https://github.com/ai-dock/base-image/wiki/2.0-Environment-Variables) for more configuration options.

### Additional Python Environments

| Environment    | Packages |
| -------------- | ----------------------------------------- |
| `comfyui`      | ComfyUI and dependencies |
| `api`          | ComfyUI API wrapper and dependencies |

The `comfyui` environment will be activated on shell login.

~~See the base micromamba environments [here](https://github.com/ai-dock/base-image/wiki/1.0-Included-Software#installed-micromamba-environments).~~

## Additional Services

The following services will be launched alongside the [default services](https://github.com/ai-dock/base-image/wiki/1.0-Included-Software) provided by the base image.

### ComfyUI

The service will launch on port `8188` unless you have specified an override with `COMFYUI_PORT_HOST`.

You can set startup flags by using variable `COMFYUI_ARGS`.

To manage this service you can use `supervisorctl [start|stop|restart] comfyui`.

### ComfyUI API Wrapper

This service is available on port `8188` and is a work-in-progress to replace previous serverless handlers which have been depreciated; Old Docker images and sources remain available should you need them.

You can access the api directly at `/ai-dock/api/` or you can use the Swager/openAPI playground at `/ai-dock/api/docs`.

>[!NOTE]
>All services are password protected by default. See the [security](https://github.com/ai-dock/base-image/wiki#security) and [environment variables](https://github.com/ai-dock/base-image/wiki/2.0-Environment-Variables) documentation for more information.

## Pre-Configured Templates

**Vast.​ai**

- [comfyui:latest-cuda](https://link.ai-dock.org/template-vast-comfyui)

- [comfyui:latest-cuda + FLUX.1](https://link.ai-dock.org/template-vast-comfyui-flux)

- [comfyui:latest-rocm](https://link.ai-dock.org/template-vast-comfyui-rocm)

---

_The author ([@robballantyne](https://github.com/robballantyne)) may be compensated if you sign up to services linked in this document. Testing multiple variants of GPU images in many different environments is both costly and time-consuming; This helps to offset costs_
