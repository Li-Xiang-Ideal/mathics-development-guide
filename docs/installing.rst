Installing Mathics
==================

.. contents::
   :depth: 1
   :local:

Here we describe the various ways to get Mathics installed.


Mathics3 (mathics-core) Requirements
------------------------------------

The Mathics suite runs on Python 3.6 or later. We also support Pyston
and PyPy 3.6 or later.

Underneath, Mathics core relies on
`SymPy <https://www.sympy.org/en/index.html>`__ which relies on
`NumPy <https://numpy.org>`__. These and the other requirements will be
installed automatically if you use the standard Python installer
`pip <https://pip.pypa.io/en/stable/>`_. They are also listed in
`setup.py <https://github.com/mathics/Mathics/blob/master/setup.py>`__.

`SciPy <https://SciPy.org/>`_ is optional. It is used for images and
provides alternative implementations for a number of builtins.

Building the PDF documentation has a number of additional dependencies.

- ``xetex`` 3.14159265-2.6-0.999991 or greater
- ``asymptote``, 2.71-37 or greater
- ``ghostscript`` Version 9.54.0 or greater

Pay close attention to the version. Some OS-provided packages have
bugs in them that will prevent certain images like those involving
opacity (used in ``Filling``) not to render.

OS package dependencies
+++++++++++++++++++++++

Here we will only describe OS package dependencies for Mathics3. For
the front-ends, Mathics-Django or mathicsscript, see the install
instructions in the specific github repositories.

Debian/Ubuntu
~~~~~~~~~~~~~

For Debian/Ubuntu based systems:

::

    $ apt-get install python-dev libsqlite3-devp python-setuptools liblapack-dev llvm-dev

as super-user, i.e. either after having issued ``su`` or by preceding
the command with ``sudo``).

Note that to build the PDF, you will need ``asymptote`` and ``.deb``
package has a couple of bugs that will cause some graphs with opacity
to fail. Asymptote version 2.71 or later is recommended. I build this
from the `git source <https://github.com/vectorgraphics/asymptote>`_.

Also ghostscript is needed and 9.50 has bugs in it too that will cause failures in
rendering Asymptote images. Use 9.54 or later.

MacOSX
~~~~~~

On Mac OS X:


::

    $ brew install sqlite3
    $ brew install llvm@11

Make sure when you install llvmlite to specify the ``LLVM_CONFIG``::

    $ LLVM_CONFIG=/usr/local/Cellar/llvm@11/11.1.0/bin/llvm-config pip install llvmlite

FreeBSD
~~~~~~~

On FreeBSD:

::

    $ sudo pkg install math/py-mathics

.. |Packaging status| image:: https://repology.org/badge/vertical-allrepos/mathics.svg
			    :target: https://repology.org/project/mathics/versions

MS Windows
~~~~~~~~~~

On Microsoft Windows:

::

      $ choco install llvm


Install from PyPI
-----------------


If you have the appropriate OS dependant packages installed, and want to install everything in one shot,
try::

       $ pip install Mathics-omnibus[full]

This might work if you don't have the full suite of support OS packages `LLVM <https://llvm.org>`_, `xetex <https://en.wikipedia.org/wiki/XeTeX>`_ and numerous others, the above may fail.

You can try a more minimal installation using::

       $ pip install Mathics-omnibus[full]

Either of these installs these suite of independent Mathics3 packages:

* ``mathicsscript``
* ``mathics-django``
* ``pymathics-graph``, ``pymathics-natlang``

These in turn pull in two other Mathics3 packages:

* ``mathics-scanner``
* ``mathics-core``


In other words, this package doesn't have any code in it. Instead it just contains dependencies to other PyPI Mathics packages.of other PyPI package.
It is more or less equivalent to::

       $ pip install Mathics3  # this is the core engine. It is a dependency of some of the below too
       $ pip install Mathics-Django[full] # web front-end with extras
       $ pip install mathicsscript[full]  # the command-line interface with extras
       $ pip install pymathics-natlang # the Natural-language Python module
       $ pip install pymathics-graph # the Python module for working with Graphs and Networks

If something fails, try using the above commands one by one, and
remove the ``[full]`` to get a more basic installation.

Note the name "Mathics3" for the core engine. This is the most recent release. "Mathics" has
pre-Python 3 code.

Other sections have descriptions of the various pieces, what
features they add and what dependencies are needed to run them.

If you want ``mathics-core`` to include modules that have been run through Cython, then install Cython separately::

     $ pip install cython

From docker (dockerhub)
-----------------------

As an alternative to building all the components from source or via Python
package, you can run pre-built code for *all* of the components via
`docker <https://www.docker.com>`__. To download a copy of the docker
image run:

::

    $ docker pull mathicsorg/mathics

This will pull the latest development release that has a docker
tagname ``#latest`` if you want a stable release, give the version in
the pull command. For example

    $ docker pull mathicsorg/mathics#4.0.0

From an OS-specific Repository
------------------------------

Click on the link below from `Repology.org <https://repology.org>`__ for
details for a specific OS and distribution.

|Packaging status|

Install from git from github
----------------------------

If you need the most recent fixes, you can install from github.  Note
that there isn't a single github repository that contains everything.

Also, since Mathics is in constant flux, dependencies can change. The
development version from might require development version from
another.

These instructions then aren't complete and may need to be adapted for
the various Mathics3 github repositories
