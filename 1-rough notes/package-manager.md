# what is a package manager
---
Date: 01,Oct,2024
subject:  package management
field: [[linux]]
tags: #apt #package #management #dnf #arch #dpkg #rpm

--- 

### What is a Package?

- A **package manager** in Linux is a tool or collection of tools that **automates the process of installing, updating, configuring, and removing software** packages. It ensures that software packages are installed correctly and that any necessary dependencies (other software required for the package to work) are also handled, making it easier for users to manage their system's software.
- In Linux, most applications are distributed as **packages**.
- A package is a bundle that contains software and the necessary files and metadata required for the software to function.
- Packages simplify the process of installing, updating, and removing software along with handling dependencies.
- Linux distributions use their own package formats, like `.deb` for Debian-based systems and `.rpm` for RHEL-based systems.
- **Repositories** are centralized locations where packages are stored.
- Most distributions have their own repositories, though third-party repositories also exist.

### Advantages

- Easily obtain the correct, trusted packages for your distribution.
- Automatically manage all dependencies.
- Enforces file conventions, such as storing configuration files in `/etc`.
- easily upgrade your packages
- can query the available packages from your terminal
- can help you rollback easily in case any thing breaks
- 

### Components of a Package

1. **Binary or Source Code**:
    
    - **Binaries**: Pre-compiled, machine-readable code that can be executed directly by the OS.
    - **Source code**: Human-readable code that gets compiled on the client system.
    - Most distros like Ubuntu, Arch, and RHEL use binary-based package managers, while distros like Gentoo and Funtoo use source code-based package managers.
2. **Metadata**:
    
    - Metadata describes the package's name, version, architecture, description, dependencies, and maintainer information.
3. **Dependencies**:
    
    - Many packages require other packages to function properly. These additional packages are called **dependencies**. Dependencies are listed in the metadata, allowing the package manager to automatically handle them.
4. **Scripts**:
    
    - Packages often contain scripts to manage installation, configuration, or removal.
        - `preinst` and `postinst` scripts are run before and after installation.
        - `prerm` and `postrm` scripts are run before and after removal.

### Type of package manager

###### Low-level package manager
	- dpkg and rpm are responsible for directly installing, removing, and managing package manually.
	- however, they don't resolve dependencies automatically.
###### High-level package manager
	- APT and YUM/DNF are like wrappers over dpkg and rpm
	- they provide aditional features like dependency resolution, package updates, repository management.

[[apt]]    [[dnf]]

> try this [make your own deb package](https://www.internalpointers.com/post/build-binary-deb-package-practical-guide)


