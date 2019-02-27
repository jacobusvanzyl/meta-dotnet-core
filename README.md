# meta-dotnet-core
BitBake recipes to use the pre-built binaries provided by Microsoft for the following applications:

1. .Net Core 2.x
2. Visual Studio Remote Debugger
  
## .Net Core 2.x
This package will place the .Net Core 2.x runtime binaries into the image under /usr/share/dotnet. The package only supports X64 and ARM (32-bit and 64-bit) architectures. It does not build the runtime from source it only pulls the publicly available binaries. Add this package by adding "dotnet-core" to the CORE_IMAGE_EXTRA_INSTALL line of your local.conf file.

## Visual Studio Remote Debugger
This package will place the vsdbg runtime binaries into the image under the root's home folder. The package only supports X64 and ARM (32-bit only) architectures. It does not build these libraries from source. These binaries are not open source. Care should be taken to ensure the proprietary license can be adhered to for the given application. Add this package by adding "vsdbg" to the CORE_IMAGE_EXTRA_INSTALL line of your local.conf file.

## Dependencies
This layer depends on:

URI | Layers | Branch
--- | ------ | ------
git://git.openembedded.org/bitbake | | rocko
git://git.openembedded.org/openembedded-core | meta | rocko
git://git.yoctoproject.org/meta | meta | rocko
git://git.openembedded.org/meta-openembedded | meta-oe | rocko
git://git.openembedded.org/meta-openembedded | meta-perl | rocko
git://git.openembedded.org/meta-openembedded | meta-python | rocko
git://git.openembedded.org/meta-openembedded | meta-networking | rocko
git://git.yoctoproject.org/meta-security | meta-security | rocko

## Patches
Please submit any patches against this layer using pull requests in github or open up an issue.

## Table of Contents
1. Adding the meta-dotnet-core to your build
2. Curl Configuration and Modification
3. Specific Versions

### 1. Adding the meta-dotnet-core to your build
In order to use this layer, you need to make the build system aware of it.

Assuming the meta-dotnet-core layer exists at the top-level of your yocto build tree, you can add it to the build system by adding the location of the layer to bblayers.conf, along with any other layers needed. e.g.:

```
  BBLAYERS ?= " \
    /path/to/yocto/meta \
    /path/to/yocto/meta-poky \
    /path/to/yocto/meta-yocto-bsp \
    /path/to/yocto/meta-dotnet-core \
    "
```

### 2. Curl Configuration and Modification
The following must be added to your local.conf file to enable specific support that is required in curl:

```
  PACKAGECONFIG_pn-curl = "vers krb5 ssl zlib ipv6"
```

NOTE: this layer will modify the curl library to contain the CURL_OPENSSL_3 versioned symbols.

### 3. Specific Versions
You can select a specific version by adding the following line to your local.conf file:

```
PREFERRED_VERSION_<package name> = "<version>"
```
  
For example:

```
PREFERRED_VERSION_dotnet-core = "2.1.3"
```

