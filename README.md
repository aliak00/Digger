# Digger

Digger can:

- build D from [git](https://github.com/D-Programming-Language)
- build older versions of D
- build D plus forks and pending pull requests
- bisect D's history to find where regressions are introduced (or bugs fixed)

Digger has a simple command-line interface, as well as a web interface for customizing your custom D build.

### Requirements

On POSIX, Digger needs git, gcc, binutils and make.

On Windows, Digger will download and unpack everything it needs (Git, DMC, 7-Zip, WiX, VS2013 and Windows SDK components).

### Get Digger

You can find binaries on the [GitHub releases](https://github.com/CyberShadow/Digger/releases) page.

### Command-line usage

##### Building D

    # build latest master branch commit
    $ digger build

    # build a specific D version
    $ digger build v2.064.2

    # build for x86-64
    $ digger build --64 v2.064.2

    # build commit from a point in time
    $ digger build "@ 3 weeks ago"

    # build latest 2.065 (release) branch commit
    $ digger build 2.065

    # build specified branch from a point in time
    $ digger build "2.065 @ 3 weeks ago"

    # build with added pull request
    $ digger build "master + dmd#123"

    # build with added GitHub fork branch
    $ digger build "master + Username/dmd/awesome-feature"

    # perform incremental build (after changing a few source files)
    $ digger rebuild

##### Bisecting

To bisect D's history to find which pull request introduced a bug, first copy `bisect.ini.sample` to `bisect.ini`, adjust as instructed by the comments, then run:

    $ digger bisect path/to/bisect.ini

### Web interface

Run digger-web to start the web interface, which allows interactively customizing a D version to build.

### Configuration

You can optionally configure a few settings using a configuration file.
To do so, copy `digger.ini.sample` to `digger.ini` and adjust as instructed by the comments.

### Building

    $ git clone --recursive https://github.com/CyberShadow/Digger
    $ cd Digger
    $ rdmd --build-only digger
    $ rdmd --build-only digger-web

On Windows, you may see:

    Warning 2: File Not Found version.lib

This is a benign warning.
