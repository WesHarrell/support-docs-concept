---
created_at: '2018-09-24T01:51:32Z'
hidden: false
label_names: []
position: 16
title: Installing (Third Party) applications
vote_count: 2
vote_sum: 2
zendesk_article_id: 360000474535
zendesk_section_id: 360000040056
---

NeSI provides a long list of various applications on its systems.
Nevertheless, if you need additional applications or libraries (below
called package), we distinguish:

-   you need a **newer version** of an already installed package: [ask
    NeSI support](https://support.nesi.org.nz/hc/en-gb/requests/new) for
    an update
-   you need an **older version** of an installed package: please use
    the Easybuild installation procedure (below) to install it into your
    working space
-   you want to test a **new (not installed)** package: below we
    collected some hints, how you can install it in your user space.

In any case, if you have issues, do not hesitate to [open a
ticket](https://support.nesi.org.nz/hc/en-gb/requests/new) and ask NeSI
support for help.

## Additional Packages for Python, R, etc.

See [Python](https://support.nesi.org.nz/hc/en-gb/articles/207782537-Python) or [R](https://support.nesi.org.nz/hc/en-gb/articles/209338087-R),
or for other languages check if we have additional documentation for it
in our [application
documentation](https://support.nesi.org.nz/hc/en-gb/sections/360000040076-Supported-Applications).

## Third party applications

Installation instruction vary from application to application. In any
case we suggest to read the provided installing instructions.
Nevertheless, the following should give you an impression which steps
you usually need to consider:

-   Change into a desired source code directory. We suggest to use
    `/nesi/nobackup/<projectID>` or `/nesi/project/<projectID>`
-   download the source code. This could be done via a repository
    checkout (`git clone <URL to the application source repository>`) or
    via downloading a tarball (`wget <URL to the tarball>`). Unpack the
    tarball using `tar xf <tar file name>`. Change into source
    directory.
-   ``load compiler module and modules for additional libraries
    (`module load gimkl FFTW`)
-   run the configure with appropriate options
    `./configure --prefix=<desired install directory> --use-fftw=$EBROOTFFTW  `(options
    can be listed using `./configure --help`)
-   In other applications you need to adjust the provided `Makefile` to
    reflect compiler, and library options (see below)
-   compile code (`make``)`
-   install the binaries and libraries into the specified directory
    (`make install`)

## Create your own modules (Optional)

You can create personalised module environments, which can load modules
and set up environment variables. For example, you could define a
modules in a project directory
`/nesi/project/<projectID>/modulefiles/ProdXY` as the following:

    #%module

    conflict ProdABC   # conflicts with other versions of itself
    module load CMake  # load other additional modules
    module load netCDF/4.4.1-gimkl-2017a
    module load Python/3.6.3-gimkl-2017a


    # provide a description
    whatis "The ProdXY for doing clever things."
    proc ModulesHelp { } {
     puts stderr "This module loads the ProdXY tool. It requires CMake and netCDF."
     puts stderr "\t the executable prodXY is provided."
    }

    # set the path to the software product (can be used later in the module)
    set PKG_PREFIX /path/to/software/package/ProdXY
    # add the location of binaries to PATH, such they are immediately accessible
    prepend-path PATH $PKG_PREFIX/bin
    # add to library path for dynamically linked applications
    prepend-path LD_LIBRARY_PATH $PKG_PREFIX/lib
    # add a location for Python packages
    prepend-path PYTHONPATH $PKG_PREFIX/lib/python3.6/site-packages/
    # for example, you can set environment variables for compiling
    setenv CFLAGS "-DNDEBUG"

In the first lines, we can set conflicts with other modules (here named
ProdABC). Then we load some dependency modules and provide some
description. The additional lines depend on your requirements for the
module. With *set* you can define internal variables (within this module
file). The command *setenv* defines a environment variable. And
*prepend-path* and *append-path* extend an environment variable at the
front or end.

There are common environment variables like:

-   *PATH* for providing executabl,
-   *LD\_LIBRARY\_PATH* for self created libraries,
-   *PYTHONPATH* for providing Python modules,
-   *CONDA\_ENVS\_PATH* for providing Conda environments,
-   etc.

And others which are very application specific.

To use the module (or all in that directory and sub-directories) we need
to register that directory to the module environment. This can be done
by setting the following environment variable:

    module use /nesi/project/<projectID>/modulefiles/ 

by adding that line to your `$HOME/.bashrc` you will have the modules
always available.

The module then can be loaded by:

    module load ProdXY

These modules can easily be shared with collaborators. They just need to
specify the last two steps.

 

 

 
