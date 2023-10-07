# papt

Personal apt: installs apt packages locally in `~/.local/`, without needing root privileges. This script installs the packages in a temp directory using `dpkg -x` and moves them to `~/.local`.

---

Usage: `./papt.sh <package-names|args>`

Arguments: <br>
`--setup`: Setups neccesarry files for installing and running these files <br>
`--help`: Display a help message

---

<sup><sub>To view earlier versions, see [tygoee/code](https://github.com/tygoee/code/blob/main/bash/local_install.sh)</sub></sup>
