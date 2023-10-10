#!/bin/bash

_help() {
    # Display a help message
    echo -e "\033[1mPapt v0.0 - Personal apt\033[0m"
    echo "Usage: $0 [options|args] command"
    echo
    echo -e "\033[1mOptions:\033[0m"
    echo "  install: Installs specified packages"
    echo
    echo -e "\033[1mArguments:\033[0m"
    echo "  --setup: Sets up necessary for installing"\
            "and running these packages"
    echo "  --help:  Display this help message"
}


_install() {
    # Install a package (and all dependencies)
    if [ $# -eq 0 ]; then
        echo "No packages specified."
        exit 1
    fi

    # Make a temp dir and cd there
    temp_dir="$HOME/.temp/"
    mkdir -p "$temp_dir"
    trap '[ -d "$HOME/.temp/" ] && rm -rf "$HOME/.temp/"' EXIT

    cd "$temp_dir" || {
        echo "Cannot CD into $temp_dir, exiting..."
        exit 1;
    }

    # Exit if there's no internet connection
    if ! ping -c 1 -W 1 "deb.debian.org" > /dev/null 2>&1; then
        echo "You need an active internet connection"
        exit 1
    fi

    # TODO: Check if all packages exist
    # and give a confirmation prompt

    # Download package and all dependencies
    for package_name in "$@"; do
        apt download "$package_name" || {
            echo "Error while trying to install package, exiting...";
            exit 1
        }

        echo "Collecting dependencies..."
        dependencies=$(apt-cache depends --recurse -i "$package_name" |
                        grep "Depends:" | awk '{print $2}' | sort -u)

        for dependency in $dependencies; do
            # TODO: Ignore virtual packages using
            # apt download .. || { apt show | grep ..; }
            apt download "$dependency"
        done
    done

    # Install all of them in .temp/install/
    for deb_file in "$temp_dir"*.deb; do
        echo "Installing ${deb_file##*/}..."
        dpkg -x "$deb_file" "install/"
    done

    # Cd into .temp/install/ and copy all files
    # to their corresponding directories
    echo "Moving files..."

    inst_dir="$temp_dir/install"
    local_dir="$HOME/.local/"
    mkdir -p "$local_dir"

    find "$inst_dir" -mindepth 1 -maxdepth 1 ! -name 'usr' -exec cp -rn {} "$local_dir" \;

    if [ -d "$inst_dir/usr/" ]; then
        find "$inst_dir/usr/" -mindepth 1 -maxdepth 1 ! -name 'local' -exec cp -rn {} "$local_dir" \;
    fi

    if [ -d "$inst_dir/usr/local/" ]; then
        cp -rn "$inst_dir/usr/local/"* "$local_dir"
    fi

    # Echo Done when the
    # installation is done
    echo "Done."
}


_setup() {
    # Setup all necessary files

    # Create all needed dirs if they dont exist
    mkdir -p "$HOME/.local/bin/"
    mkdir -p "$HOME/.local/lib/"
    mkdir -p "$HOME/.local/lib64/"
    mkdir -p "$HOME/.local/lib/x86_64-linux-gnu/"

    echo "Created library directories..."

    # Add the library path to .profile
    # if --setup is specified
    lib_paths="$(printf '%s' \
        "export LD_LIBRARY_PATH=" \
        "$HOME/.local/lib:" \
        "$HOME/.local/lib64:" \
        "$HOME/.local/lib/x86_64-linux-gnu")"

    # Append to $HOME/.profile
    # if it isn't already there
    if ! grep -q "$lib_paths" \
            "$HOME/.profile"; then
        echo "Adding library paths..."
        echo "$lib_paths" >> "$HOME/.profile"
        eval "$lib_paths"
        echo "Please reboot your computer or"\
                "login again to complete the setup"
    else
        echo "Library paths already"\
                "present, ignoring..."
    fi

    echo "Done."
}


_syntaxerr() {
    echo "Usage: $0 [options|args] command"
    echo "See --help for more info"
    exit 1
}


# Exit if there are no arguments
if [ $# -eq 0 ]; then
    _syntaxerr
fi

# Execute the right command
case "$1" in
  # Arguments
  --help)
    _help
    ;;
  --setup)
    _setup
    ;;

  # Options
  install)
    _install "${@:2}"
    ;;

  # None of these
  *)
    _syntaxerr
    ;;
esac