# Overview

Meestic is a small utility made to control **the lights of MSI Delta 15 laptop keyboards** on Windows and Linux. It provides both a CLI and a system-tray GUI, and can fully replace the official MSI tool (which is not even available for Linux).

You can use the command-line or the GUI version. Download ready-to-use binaries from the [release section of this repository](https://github.com/Koromix/meestic/releases/latest).

It was made by looking at the HID packets sent by the Windows tool with Wireshark. It is provided "as is", I don't make any guarantee about this tool.

Use the following links for more information:

- Documentation: https://koromix.dev/meestic
- Changelog: https://github.com/Koromix/rygel/blob/master/src/meestic/CHANGELOG.md

Up-to-date binaries are available here:

- [Windows](https://download.koromix.dev/windows/)
- [Linux (Debian)](https://koromix.dev/meestic#linux-debian)
- [Linux (RPM)](https://koromix.dev/meestic#linux-rpm)

# Source code

This repository does not contain the code of Meestic but only exists as a front. For pratical reasons, I've started using a single repository for all my projects in 2018 because it is easier to manage.

The source code is available here: https://github.com/Koromix/rygel/ (in the *src/meestic* subdirectory).

Monorepositories have two killer features for me:

- Cross-project refactoring
- Simplified dependency management

You can find a more detailed rationale here: https://danluu.com/monorepo/
