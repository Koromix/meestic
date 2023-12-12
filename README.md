# Overview

Meestic is a small utility made to control **the lights of MSI Delta 15 laptop keyboards** on Windows and Linux. It provides both a CLI and a system-tray GUI, and can fully replace the official MSI tool (which is not even available for Linux).

You can use the command-line or the GUI version. Download ready-to-use binaries from the [release section of this repository](https://github.com/Koromix/meestic/releases/latest).

It was made by looking at the HID packets sent by the Windows tool with Wireshark. It is provided "as is", I don't make any guarantee about this tool.

Use the following links for more information:

- Documentation: https://koromix.dev/meestic
- Source code: https://github.com/Koromix/rygel/ (see below for an explanation)

# Install

## Windows

Download ready-to-use binaries from the release section of the [dedicated repository](https://github.com/Koromix/meestic/releases).

## macOS

Download ready-to-use binaries from the release section of the [dedicated repository](https://github.com/Koromix/meestic/releases).

## Linux

A signed Debian repository is provided, and should work with Debian 11 and Debian derivatives (such as Ubuntu).

Execute the following commands (as root) to add the repository to your system:

```sh
mkdir -p -m0755 /etc/apt/keyrings
curl https://download.koromix.dev/debian/koromix-archive-keyring.gpg -o /etc/apt/keyrings/koromix-archive-keyring.gpg
echo "deb [signed-by=/etc/apt/keyrings/koromix-archive-keyring.gpg] https://download.koromix.dev/debian stable main" > /etc/apt/sources.list.d/koromix.dev-stable.list
```

Once this is done, refresh the repository cache and install the package:

```sh
apt update
apt install meestic
```

For other distributions, you can [build the code from source](https://koromix.dev/meestic#build_from_source) as documented on the website.

# Source code

This repository does not contain the code of Meestic but only exists as a front. For pratical reasons, I've started using a single repository for all my projects in 2018 because it is easier to manage.

The source code is available here: https://github.com/Koromix/rygel/ (in the *src/meestic* subdirectory).

Monorepositories have two killer features for me:

- Cross-project refactoring
- Simplified dependency management

You can find a more detailed rationale here: https://danluu.com/monorepo/

# Usage

## Command-line version

Here are a few examples on how to use it:

```sh
# Disable lighting
meestic -m Disabled

# Set default static MSI blue
meestic -m Static MsiBlue

# Slowly breathe between Orange and MsiBlue
meestic -m Breathe -s 0 "#FFA100" MsiBlue

# Quickly transition between Magenta, Orange and MsiBlue colors
meestic -m Transition -s 2 Magenta Orange MsiBlue
```

Use `meestic --help` for a list of available options.

Be careful, color names and most options are **case-sensitive**.

## Configure GUI profiles

### Windows

Create a file named `MeesticGui.ini` to customize the profiles, and put it either:

- Next to `MeesticGui.exe`
- Or at `<ProfileDir>\AppData\MeesticGui.ini` (e.g. _C:\Users\JohnDoe\AppData\MeesticGui.ini_)

Restart the GUI to apply each change.

### Linux

After installing the Debian package, edit `/etc/meestic.ini`. Once done, restart the daemon with `sudo systemctl restart meestic`.

### Example

Here is an example:

```ini
# The profile set with Default will run when the GUI starts
Default = Disabled

[Static Blue]
Mode = Static
Colors = MsiBlue

[Breathe Slow]
Mode = Breathe
Speed = 0
Colors = #FFA100 MsiBlue

[Disabled]
Mode = Disabled

# [Example]
# Intensity = 0 to 10
# Speed = 0 to 2
# Mode = Disabled, Static, Breathe or Transition
# Colors = list of Colors (only one for Static, 1 to 7 for Breathe or Transition), use name or CSS-like hexadecimal
# ManualOnly = Yes or No (if Yes, the option must be used from the context menu and won't be used when cycling modes with the function keys)
```
