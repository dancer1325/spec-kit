# Installing -- via -- pipx

* steps
  * install [pipx](https://pipx.pypa.io/)
  * install Specify CLI

    ```bash
    # install the latest
    pipx install git+https://github.com/github/spec-kit.git
    
    # install a specific stable release
    pipx install git+https://github.com/github/spec-kit.git@vX.Y.Z
    ```
    * `specify version`
      * verify installation

## Upgrade

```bash
pipx install --force git+https://github.com/github/spec-kit.git@vX.Y.Z
```

## Uninstall

```bash
pipx uninstall specify-cli
```
