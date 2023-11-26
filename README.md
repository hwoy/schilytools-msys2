# Schily-Tools-MSYS2

This repository provides patches to build [Schily-Tools](http://schilytools.sourceforge.net/) with [MSYS2](https://www.msys2.org/).


## Introduction

[Schily-Tools](http://schilytools.sourceforge.net/) is a collection of tools inspired by SunOS developed and maintained by [Joerg Schilling](http://cdrtools.sourceforge.net/private/).
This software package is also famous for cdrtools.
The patch file distributed via this repository allows you to build [Schily-Tools](http://schilytools.sourceforge.net/) on the [MSYS2](https://www.msys2.org/) (neither MinGW32 nor MinGW64) environment.


## Preparation

Please install the following packages in advance:

* base-devel,
* msys2-devel,
* msys2-runtime-devel.

This document also assumes that

* you are working in the home directory ($HOME) in MSYS2,
* [the tarball](https://sourceforge.net/projects/schilytools/) is saved as ~/schily-2021-09-18.tar.bz2,
* the local copy of this repository locates in ~/schilytools-msys2.

## defs_h-schily-msys2.patch
* ```SIG2STR_MAX``` in defs.h cause compile error.
```c
/* signal.h */
#if __SIZEOF_INT__ >= 4
#define SIG2STR_MAX (sizeof("RTMAX+") + sizeof("4294967295") - 1)
#else
#define SIG2STR_MAX (sizeof("RTMAX+") + sizeof("65535") - 1)
#endif
```
* ```(sizeof("RTMAX+") + sizeof("4294967295") - 1)``` cause of error.

## Installation

```console
$ tar xvjf ~/schily-2021-09-18.tar.bz2
$ cd ~/schily-2021-09-18
$ patch -p1 < ~/schilytools-msys2/diff_c-schily-msys2.patch
$ patch -p1 < ~/schilytools-msys2/defs_h-schily-msys2.patch
$ cd ~/schily-2021-09-18/psmake
$ ./MAKE-all
$ cd ..
$ psmake/smake
$ psmake/smake install
```

In default, the tools are installed into /opt/schily.
Please issue

```console
$ psmake/smake INS_BASE=/usr/local/schily install
```

If you want the tools to be installed in /usr/local/schily instead.

## RIP
* jörg schilling

### Contact me
- Web: https://github.com/hwoy 
- Email: zaintcorp@yahoo.com 
- Facebook: http://www.facebook.com/watt.duean
