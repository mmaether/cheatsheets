# Windows Subsystem for Linux (WSL)

The Windows Subsystem for Linux lets developers run a GNU/Linux environment -- including most command-line tools, utilities, and applications -- directly on Windows, unmodified, without the overhead of a traditional virtual machine or dualboot setup.

## Installation

Before installing any Linux distributions on Windows, you must enable the "Windows Subsystem for Linux" optional feature.

Open PowerShell as Administrator and run:

`dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`

Alternatively you can go to "Turn Windows features on or off" and select "Windows Subsystem for Linux", click OK, then reboot.

## Commands

Command | Description
------- | -----------
`wsl -l` | Lists installed WSL distributions, e.g. Ubuntu.
`wsl` | Launches the default Linux distribution.
`wsl --help` | View help documentation.
`wsl -u root` | Open PowerShell and enter the root of your default WSL distribution using this command.
`passwd` | Reset your Linux password once entered.
`wsl --set-default-version 2` | Set WSL 2 as the default version when installing a new Linux distribution.
