# ksm v1.6-dev [![Build Status](https://img.shields.io/travis/asamy/ksm/master.svg?style=flat-square&label=Linux)](https://travis-ci.org/asamy/ksm) [![Build Status](https://img.shields.io/appveyor/ci/asamy/ksm/master.svg?style=flat-square&label=Windows)](https://ci.appveyor.com/project/asamy/ksm) <a href="https://scan.coverity.com/projects/asamy-ksm"><img alt="Coverity Scan Build Status" src="https://scan.coverity.com/projects/10823/badge.svg"/> </a> [![BountySource](https://www.bountysource.com/badge/team?team_id=189129&style=raised)](https://www.bountysource.com/teams/ksm?utm_source=ksm&utm_medium=shield&utm_campaign=raised)  

A really simple and lightweight x64 hypervisor written in C for Intel processors.  
KSM has a self-contained physical memory introspection engine and userspace physical
memory virtualization which can be enabled at compiletime.

Currently, KSM runs on Windows and Linux kernels natively, and aims to support
macOS by 2017, if you want to port KSM see `Documentation/SPEC.rst` for more information.

**Note**: You can find Windows 10 precompiled binaries [here](https://ci.appveyor.com/project/asamy/ksm).  

## Purpose

Unlike other hypervisors (e.g. KVM, XEN, etc.), KSM's purpose is not to run
other Operating Systems, instead, KSM can be used as an extra layer of
protection to the existing running OS.  This type of virtualization is usually
seen in Anti-viruses, or sandboxers or even Viruses.  KSM also supports
nesting, that means it can emulate other hardware-assisted virtualization tools
(VT-x).

## Usage under Linux (+sandbox)

[![asciicast](https://asciinema.org/a/10cu6v7c6l0j4532cww8tq1a1.png)](https://asciinema.org/a/10cu6v7c6l0j4532cww8tq1a1)

## Features

- IDT Shadowing
- EPT violation #VE (Disabled when unavailable - At least Broadwell required)
- EPTP switching VMFUNC (Emulated when unavailable - At least Haswell required)
- APIC virtualization (Experimental, do not use)
- VMX Nesting (Experimental, do not use)
- Builtin Userspace physical memory sandboxer (Optional)
- Builtin Introspection engine (Optional)

## Requirements

- An Intel processor (with VT-x and EPT support)
- A working C compiler (GCC or Microsoft compiler aka CL are supported)

## Supported Kernels

- Windows NT kernel (7/8/8.1/10)
- Linux kernel (tested under 3.16, 4.8.13 and mainline)

## Documentation

- [Building](https://github.com/asamy/ksm/blob/master/Documentation/BUILDING.rst)
- [Contributions](https://github.com/asamy/ksm/blob/master/Documentation/CONTRIBUTIONS.rst)
- [Specification](https://github.com/asamy/ksm/blob/master/Documentation/SPEC.rst)
- [TODO](https://github.com/asamy/ksm/blob/master/Documentation/TODO.rst)

## Module integration

Few modular examples are included to illustrate usage, those are:

- `epage.c` - A shadow executale page hooking mechanism using multiple EPTP.
- `introspect.c` - A small and stupid physical memory introspection engine using EPT.
- `sandbox.c` - A small, incomplete and simple userspace physical memory sandbox.

See Documentation/BUILDING.rst on how to enable those modules while building.

## Issues (bugs, features, etc.)

Feel free to use Github Issues, there is an Issue Template to help you file
things as required.

## References

- Linux kernel (KVM)
- HyperPlatform
- XEN

## License

GPL v2, see LICENSE file.  Note that some code is thirdparty, respective
licenses and/or copyright should be there, if you think otherwise, feel free to mail me.
