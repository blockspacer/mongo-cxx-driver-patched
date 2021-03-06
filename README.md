# About

patched to support "zlib/v1.2.11@conan/stable" with "openssl/OpenSSL_1_1_1-stable@conan/stable"

## Local build

```bash
export CC=clang-6.0
export CXX=clang++-6.0

$CC --version
$CXX --version

# use version from conan
(sudo apt remove *gflag* || true)

conan remote add conan-center https://api.bintray.com/conan/conan/conan-center False

export PKG_NAME=mongo-cxx-driver/3.3.0@dev/stable

(CONAN_REVISIONS_ENABLED=1 \
    conan remove --force $PKG_NAME || true)

CONAN_REVISIONS_ENABLED=1 \
    CONAN_VERBOSE_TRACEBACK=1 \
    CONAN_PRINT_RUN_COMMANDS=1 \
    CONAN_LOGGING_LEVEL=10 \
    GIT_SSL_NO_VERIFY=true \
    conan create . dev/stable -s build_type=Debug --profile clang --build missing -o openssl:shared=True

CONAN_REVISIONS_ENABLED=1 \
    CONAN_VERBOSE_TRACEBACK=1 \
    CONAN_PRINT_RUN_COMMANDS=1 \
    CONAN_LOGGING_LEVEL=10 \
    conan upload $PKG_NAME --all -r=conan-local -c --retry 3 --retry-wait 10 --force

# clean build cache
conan remove "*" --build --force
```

## Package Status

| Bintray | Windows | Linux & macOS |
|:--------:|:---------:|:-----------------:|
|[![Download](https://api.bintray.com/packages/bincrafters/public-conan/mongo-cxx-driver%3Abincrafters/images/download.svg) ](https://bintray.com/bincrafters/public-conan/mongo-cxx-driver%3Abincrafters/_latestVersion)|[![Build status](https://ci.appveyor.com/api/projects/status/github/bincrafters/conan-mongo-cxx-driver?svg=true)](https://ci.appveyor.com/project/bincrafters/conan-mongo-cxx-driver)|[![Build Status](https://travis-ci.com/bincrafters/conan-mongo-cxx-driver.svg)](https://travis-ci.com/bincrafters/conan-mongo-cxx-driver)|

## Conan.io Information

Bincrafters packages can be found in the following public Conan repository:

[Bincrafters Public Conan Repository on Bintray](https://bintray.com/bincrafters/public-conan)

*Note: You can click the "Set Me Up" button on the Bintray page above for instructions on using packages from this repository.*

## Issues

If you wish to report an issue or make a request for a Bincrafters package, please do so here:

[Bincrafters Community Issues](https://github.com/bincrafters/community/issues)

## General Information

This GIT repository is managed by the Bincrafters team and holds files related to Conan.io.  For detailed information about Bincrafters and Conan.io, please visit the following resources:

[Bincrafters Wiki - Common README](https://github.com/bincrafters/community/wiki/Common-README.md)

[Bincrafters Technical Documentation](http://bincrafters.readthedocs.io/en/latest/)

[Bincrafters Blog](https://bincrafters.github.io)

## License Information

Bincrafters packages are hosted on [Bintray](https://bintray.com) and contain Open-Source software which is licensed by the software's maintainers and NOT Bincrafters.  For each Open-Source package published by Bincrafters, the packaging process obtains the required license files along with the original source files from the maintainer, and includes these license files in the generated Conan packages.

The contents of this GIT repository are completely separate from the software being packaged and therefore licensed separately.  The license for all files contained in this GIT repository are defined in the [LICENSE.md](LICENSE.md) file in this repository.  The licenses included with all Conan packages published by Bincrafters can be found in the Conan package directories in the following locations, relative to the Conan Cache root (`~/.conan` by default):

### License(s) for packaged software:

    ~/.conan/data/<pkg_name>/<pkg_version>/bincrafters/package/<random_package_id>/license/<LICENSE_FILES_HERE>

*Note :   The most common filenames for OSS licenses are `LICENSE` AND `COPYING` without file extensions.*

### License for Bincrafters recipe:

    ~/.conan/data/<pkg_name>/<pkg_version>/bincrafters/export/LICENSE.md