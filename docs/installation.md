# Installation Guide

* OFFICIAL distribution channels
  * [github/spec-kit](https://github.com/github/spec-kit)
    * ⚠️ONLY OFFICIAL maintained repository⚠️
      * ❌NOT packages | PyPI❌
  * TODO: [`specify-cli`](https://pypi.org/project/specify-cli/) package on [PyPI](https://pypi.org/project/specify-cli/)

## ⚠️Prerequisites⚠️

* OS
  * Linux
  * macOS
  * Windows
    * RIGHT NOW (BUT NOT from the scratch)
      * Reason:🧠PowerShell scripts were NOT supported🧠
* [AI coding agent](supportedAIAgents.md)
* [uv](https://docs.astral.sh/uv/) 
  * Reason:🧠package management🧠
* [Python 3.11+](https://www.python.org/downloads/)
* [Git](https://git-scm.com/downloads)

## how to install?

### PERSISTENT

* 👀recommended one👀
  * Reason:🧠NO re-download | EACH invocation🧠
* ways
  * [-- via -- uv](install/uv.md)
  * [-- via -- pipx](install/pipx.md)
  * [-- via -- Enterprise / Air-Gapped](install/air-gapped.md)

### 1-time Usage

* [-- through -- `uvx`](install/one-time.md)

## how to initialize Github SpecKit | project?

* steps
  * run the command 

    ```bash
    # MULTIPLE ways
    # 1. <PROJECT_NAME>
    # 1.1   | PERSISTENT Installation
    specify init <PROJECT_NAME> [OPTIONS]
    # 1.2   | 1-time Usage Installation
    # 1.2.1   latest
    uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME> [OPTIONS]
    # 1.2.2   specific version
    uvx --from git+https://github.com/github/spec-kit.git@vX.Y.Z specify init <PROJECT_NAME> [OPTIONS]
    
    # 2. | CURRENT directory
    # 2.1   | PERSISTENT Installation
    specify init . [OPTIONS]
    # 2.2   | 1-time Usage Installation
    # 2.2.1   latest
    uvx --from git+https://github.com/github/spec-kit.git specify init . [OPTIONS]
    # 2.2.2   specific version
    uvx --from git+https://github.com/github/spec-kit.git@vX.Y.Z specify init . [OPTIONS]
    
    # 3. --here   == 2.
    # 3.1   | PERSISTENT Installation 
    specify init --here [OPTIONS]
    # 3.2   | 1-time Usage Installation
    # 3.2.1   latest
    uvx --from git+https://github.com/github/spec-kit.git specify init --here [OPTIONS]
    # 3.2.2   specific version
    uvx --from git+https://github.com/github/spec-kit.git@vX.Y.Z specify init --here [OPTIONS]
    ```
  * | terminal prompts, choose options
  * [`[OPTIONS]`](reference/core.md)

### verification

* [`specify version`](reference/core.md)
* [`/speckit.*` commands / AVAILABLE | your AI agent](cli.md)
* ".specify/scripts/"
  * == ALL `.sh` & `.ps1` scripts
