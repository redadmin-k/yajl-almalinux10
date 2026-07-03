# YAJL RPM for AlmaLinux 10

This repository provides an unofficial YAJL RPM package for AlmaLinux 10.

The package was rebuilt for AlmaLinux 10 from the AlmaLinux 9 source RPM.

This package is mainly intended as a dependency for local ModSecurity v3 builds and installation on AlmaLinux 10.

## Overview

YAJL is required by ModSecurity.

On AlmaLinux 10, YAJL may not be available in the default repositories depending on the environment.

This repository provides rebuilt YAJL RPMs for AlmaLinux 10.

Included packages:

```text
yajl-2.1.0-25.el10.x86_64.rpm
yajl-devel-2.1.0-25.el10.x86_64.rpm
yajl-debuginfo-2.1.0-25.el10.x86_64.rpm
yajl-debugsource-2.1.0-25.el10.x86_64.rpm
yajl-2.1.0-25.el10.src.rpm
```

For normal ModSecurity installation or build usage, only these packages are usually required:

```text
yajl-2.1.0-25.el10.x86_64.rpm
yajl-devel-2.1.0-25.el10.x86_64.rpm
```

## Install

Install the runtime and development packages with:

```bash
sudo dnf localinstall \
  yajl-2.1.0-25.el10.x86_64.rpm \
  yajl-devel-2.1.0-25.el10.x86_64.rpm
```

If the RPM files are stored under an `RPMS/` directory, use:

```bash
sudo dnf localinstall \
  RPMS/yajl-2.1.0-25.el10.x86_64.rpm \
  RPMS/yajl-devel-2.1.0-25.el10.x86_64.rpm
```

A more general command is:

```bash
sudo dnf localinstall $(find . -type f \( -name 'yajl-*.rpm' -o -name 'yajl-devel-*.rpm' \) | grep -v debuginfo | grep -v debugsource | sort)
```

## Verify Installation

Check installed packages:

```bash
rpm -q yajl yajl-devel
```

Check installed files:

```bash
rpm -ql yajl
rpm -ql yajl-devel
```

## Usage with ModSecurity

This package can be used as a dependency for ModSecurity v3 on AlmaLinux 10.

ModSecurity spec files commonly require:

```spec
BuildRequires:  yajl-devel
Requires:       yajl
```

Install YAJL before building or installing ModSecurity:

```bash
sudo dnf localinstall \
  yajl-2.1.0-25.el10.x86_64.rpm \
  yajl-devel-2.1.0-25.el10.x86_64.rpm
```

Then build or install the ModSecurity RPM.

## Package Notes

The following packages are not required for normal installation:

```text
yajl-debuginfo-*.rpm
yajl-debugsource-*.rpm
yajl-*.src.rpm
```

They are provided for debugging, source reference, or rebuild purposes.

## Target Environment

Tested target environment:

```text
AlmaLinux 10
x86_64
YAJL 2.1.0
ModSecurity v3 dependency usage
```

## Disclaimer

This repository is unofficial.

It is not provided, maintained, endorsed, or supported by AlmaLinux OS Foundation or the upstream YAJL project.

Use this repository at your own risk.

The author provides no warranty of any kind.

Please test carefully in a verification environment before using it in production.

## License

YAJL is distributed under its upstream license.

See the source RPM or upstream YAJL project for license details.

Packaging files and rebuild notes in this repository are provided for RPM build and integration testing purposes.
