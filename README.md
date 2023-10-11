# Papt - Personal apt

Personal apt: installs apt packages locally in `~/.local/`, without needing root privileges. This script installs the packages in a temp directory using `dpkg -x` and moves them to `~/.local/`.

> **IMPORTANT**
> This is still in very early development and could break your `~/.local/` folder. I recommend using this in a virtual machine or other seperated environment.

## Installation

First, clone the repository and cd there:

    git clone https://github.com/tygoee/papt
    cd papt

If you want this to be available as a command, copy it to `~/.local/bin/`:

    mkdir -p ~/.local/bin/
    cp ./papt ~/.local/bin/

Finally, setup papt:

    papt --setup

## Usage

Command usage: `papt [options|args] command`

**Options:**  
`install`: Installs specified packages

**Arguments:**  
`--setup`: Sets up necessary files for installing and running these packages  
`--help`: Display a help message

## Credits

Also see [tedrek/papt](https://github.com/tedrek/papt), I noticed his project after starting with mine, but saw it was pretty abandoned.

If you want a place in this section, feel free to contribute :)

---

© Tygo Everts | 2023  
This code is licensed under the MIT License.  
For more details, see [LICENSE](/LICENSE).

<sup><sub>To view earlier versions, see [tygoee/code](https://github.com/tygoee/code/blob/main/bash/local_install.sh)</sub></sup>
