# NVIDIA Nemotron Fine-Tuning 

## About this project

[Nemotron-3 8B model](https://huggingface.co/nvidia/nemotron-3-8b-base-4k) is a robust, powerful family of Large Language Models that can provide compelling responses on a wide range of tasks. While the 8B parameter base model serves as a strong baseline for multiple downstream tasks, they can lack in domain-specific knowledge or proprietary or otherwise sensitive information. Fine-tuning is often used as a means to update a model for a specific task or tasks to better respond to domain-specific prompts. 

In this project we demonstrate how to use [NVIDIA's NeMo Toolkit](https://www.nvidia.com/en-us/ai-data-science/products/nemo/) to fine-tune the Nemotron-3 model. The attached notebook walks through preparing a dataset, using Low Rank Adaptation (LoRA) to do some fine-tuning, and then finish by running sample sample data through the newly fine-tuned model.

## Set up instructions

This project requires the following [compute environments](https://docs.dominodatalab.com/en/latest/user_guide/f51038/environments/) to be present.

### Hardware Requirements
You also need to make sure that the hardware tier running the notebook or the fine-tuning script has sufficient resources. A GPU with >=120GB of VRAM is recommended. This project was tested on an `A100` with **120GB** VRAM. 

### Environment Requirements

**Base image :** `nvcr.io/nvidia/nemo:24.01.framework`

**Dockerfile Instructions**

These instructions are added automatically by selecting the "Automatically make compatible with Domino" checkbox while creating the environment.

```
# System-level dependency injection runs as root
USER root:root

# Validate base image pre-requisites
# Complete requirements can be found at
# https://docs.dominodatalab.com/en/latest/user_guide/a00d1b/automatic-adaptation-of-custom-images/#_pre_requisites_for_automatic_custom_image_compatibility_with_domino
RUN /opt/domino/bin/pre-check.sh

# Configure /opt/domino to prepare for Domino executions
RUN /opt/domino/bin/init.sh

# Validate the environment
RUN /opt/domino/bin/validate.sh
```

**Pluggable Workspace Tools** 
```
jupyterlab:
  title: "JupyterLab"
  iconUrl: "/assets/images/workspace-logos/jupyterlab.svg"
  start: [ "/opt/domino/workspaces/jupyterlab/start" ]
  httpProxy:
    internalPath: "/{{ownerUsername}}/{{projectName}}/{{sessionPathComponent}}/{{runId}}/{{#if pathToOpen}}tree/{{pathToOpen}}{{/if}}"
    port: 8888
    rewrite: false
    requireSubdomain: false
vscode:
 title: "vscode"
 iconUrl: "/assets/images/workspace-logos/vscode.svg"
 start: [ "/opt/domino/workspaces/vscode/start" ]
 httpProxy:
    port: 8888
    requireSubdomain: false
```