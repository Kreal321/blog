---
title: PuTTY
tags:
  - Tool
  - SSH
  - PuTTY
  - Mac
---

## How to use PuTTY on Mac

1. Install PuTTY

    Install PuTTY using `brew` or `port`. This will also install the command-line version of puttygen (the PuTTY key generator tool).

    ```zsh
    brew install putty
    ```

    Or

    ``` zsh
    port install putty
    ```

2. Using PEM formate private key

    Convert the `.ppk` format private key to a standard `.pem` format private key

    ```zsh
    puttygen privatekey.ppk -O private-openssh -o privatekey.pem
    ```

    Grant readable pression

    ```zsh
    chmod go-rw privatekey.pem
    ```

3. Use the key for login

    ```zsh
    ssh -i privatekey.pem user@hostname
    ```

