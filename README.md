# Papt - Personal apt

Personal apt: installs apt packages locally in `~/.local/`, without needing root privileges. This script installs the packages in a temp directory using `dpkg -x` and moves them to `~/.local/`.

## Installation

First, clone the repository and cd there:

    git clone https://github.com/tygoee/papt
    cd papt

If you want this to be available as a command, copy it to `~/.local/bin/`:

    mkdir -p ~/.local/bin/
    cp ./papt.sh ~/.local/bin/papt

Finally, setup papt:

    papt --setup

## Usage

Command usage: `papt [options|args] command`

**Options:** <br>
`install`: Installs specified packages

**Arguments:** <br>
`--setup`: Sets up necessary files for installing and running these packages <br>
`--help`: Display a help message

---

<sup><sub>To view earlier versions, see [tygoee/code](https://github.com/tygoee/code/blob/main/bash/local_install.sh)</sub></sup>
