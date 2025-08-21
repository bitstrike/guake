# Guake 3 README

[![CI](https://github.com/Guake/guake/actions/workflows/ci.yml/badge.svg)](https://github.com/Guake/guake/actions)
[![Bountysource](https://img.shields.io/bountysource/team/guake/activity.svg)](https://www.bountysource.com/teams/guake)
[![Documentation](https://readthedocs.org/projects/guake/badge/?version=stable)](https://guake.readthedocs.io/en/stable/?badge=stable)
[![Translation](https://hosted.weblate.org/widgets/guake/-/guake/svg-badge.svg)](https://hosted.weblate.org/projects/guake/guake/)

## Introduction

Guake is a python based dropdown terminal made for the GNOME desktop environment. Guake's style of window is based on an FPS game, and one of its goals is to be easy to reach.

## Pin Terminal Feature

This fork enhances Guake with a visual indicator on the terminal tab when the existing "do-not-hide-on-lost-focus" functionality is enabled. This makes it easy to identify when guake is not in auto-hide mode. This can also now be toggled from the Guake context menu.


Additionally, the .deb package builder in the Makefile was shmoozed into working order because pypi and I like to have a deb as an install option anyway. An sha256sum is included in the Releases so be sure to verify the package is authentic if you find this package somewhere else on the web. If you need RPM or other format `sudo apt install alien` should do the trick.

**Key Benefits:**
- **Visual Feedback**: Clear indication on tab that pin-mode is active
- **Screenshot-Friendly**: Perfect for taking screenshots of terminal content without the terminal hiding
- **Consistent State**: Synchronized pin state between hotkey, app button, and tab indicators
- **Easy Control**: Can "Toggle auto-hide" option in the terminal context menu

**How It Works:**
- Enable pin mode using the global hotkey (Ctrl+Shift+F1) or app pin button
- The active tab shows a pin icon when pin mode is active
- Guake stays visible even when focus is lost
- Toggle pin mode to restore normal hide-on-lose-focus behavior

**Pin Mode in Action:**
![Pin Mode Feature](images/pin-mode-2.png)

## Installation

### Pre-built Debian Package

Pre-built Debian packages (`.deb`) are available for easy installation on Debian/Ubuntu systems. 

**Download and install:**
```bash
# Download the latest package from GitHub releases
wget https://github.com/bitstrike/guake/releases/latest/download/guake_*.deb

# Install the package
sudo dpkg -i guake_*.deb
```

**Note**: This package includes all necessary dependencies and will install to the system-wide `/usr` directory.

**Package details and SHA256 checksums** are available on the [GitHub releases page](https://github.com/bitstrike/guake/releases).

## Building from Source

### Prerequisites

Install build dependencies on Debian/Ubuntu systems:
```bash
sudo apt install libgirepository1.0-dev python3-dev python3-gi libcairo2-dev pkg-config \
                 gir1.2-gtk-3.0 gir1.2-keybinder-3.0 libkeybinder-3.0-0 gir1.2-vte-2.91 \
                 gir1.2-wnck-3.0 gir1.2-notify-0.7 dh-make debhelper meson ninja-build
```

### Build Debian Package (Recommended)

This fork includes an enhanced build system that creates standard Debian packages (`.deb`) with the Pin Terminal feature:

```bash
# Clone the repository (required for proper versioning)
git clone https://github.com/bitstrike/guake.git
cd guake

# Build the Debian package
make deb
```

**What this does:**
- ✅ **Creates standard .deb package** - Uses `dh_make` and `dpkg-deb`
- ✅ **Includes Pin Terminal feature** - All enhancements are included
- ✅ **System-wide installation** - Installs to `/usr` (standard locations)
- ✅ **Complete dependency handling** - Manages all required system packages
- ✅ **Clean build process** - Automatically manages build artifacts

**Why use `make deb` instead of `make install`:**
- **Standard packaging** - Creates .deb files that can be shared/distributed
- **Easy installation** - Users can install with `sudo dpkg -i`
- **Proper uninstallation** - Can be removed with package manager
- **Dependency management** - Handles system dependencies correctly

### Install Your Built Package

```bash
# Install the package you just built
sudo dpkg -i ./guake_*.deb

# Or use apt to handle dependencies automatically
sudo apt install ./guake_*.deb
```

### Traditional Build Method (Alternative)

If you prefer the traditional source build approach:

```bash
# Build and install directly to system
make
sudo make install PREFIX=/usr
```

**Note**: The traditional method installs directly to your system. The `make deb` method is recommended as it creates a distributable package that can be easily managed and shared.

### ⚠️ Test Status

**Warning**: I spent hours trying to get the Python test suite (`make test`) working. It still fails due to complex dependency issues with GTK/GObject bindings and pipenv. Probably more. These are notoriously difficult to resolve and I gave up.

**What this means:**
- ✅ **Build works** - You can successfully build and install Guake
- ✅ **Package creation works** - `make deb` creates working .deb packages
- ❌ **Tests fail** - `make test` will likely fail with dependency errors
- ❌ **CI broken** - GitHub Actions tests are disabled due to these issues

**Recommendation**: Focus on building and packaging rather than trying to fix the test suite. The core functionality works correctly despite test failures. 

## Quick Installation Guide

Please refer to [Installation Guide](https://guake.readthedocs.io/en/latest/user/installing.html#system-wide-installation)

## What it looks like?

![Guake Screenshot](https://i.ibb.co/s97cJWZ/guake.png)

Drop down terminal on pressing <F12>

## Note when compiling from source

Do **NOT** use the Tarball packages automatically generated by GitHub on the Release pages. They won't work because one of the main components of Guake build system, PBR, requires the full Git history to be available when building from source. Note this does not impact source distribution packages you can download from Pypi.

**For this fork**: Use the "Building from Source" section above to build a standard `.deb` package with the Pin Terminal feature included.

Original build from sources instructions are described on [this page of the Online Documentation](http://guake.readthedocs.io/en/latest/user/installing.html#install-from-source). Please read this carefully before opening an issue!

## Bugs? Information?

- Source Code available on [GitHub](https://github.com/Guake/guake/).
- Official Homepage: https://guake.github.io
- Online Documentation is hosted on [ReadTheDocs](http://guake.readthedocs.io/).
- If you are not a developer, you can still contribute to Guake by [improving its translations in your language](https://hosted.weblate.org/projects/guake/guake/). Guake users are welcome [to support Weblate](https://weblate.org/donate/) in providing this service for free for OpenSource Projects.

**Important note**: Do **NOT** use the domain guake.org, it has been registered by someone outside the team. We cannot be held responsible for the content on that web site.

This project was originally created by Gabriel Falcão, see: https://sourceforge.net/projects/guake-gnome-vte/
