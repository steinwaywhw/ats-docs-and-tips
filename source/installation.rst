******************
Installation
******************

Install ATS 2 from Source Code
===============================

Before installing ATS 2, we need the latest version of ATS 1 first. 

#. Download ATS 0.2.10 from http://www.cs.bu.edu/~hwxi/ATS/IMPLEMENTATION/Anairiats/ats-lang-anairiats-0.2.10-unstable.tgz
#. Unzip it into a folder, e.g. ``~/ats``
#. Setup environment variables

	.. code-block:: bash

		export ATSHOME=~/ats
		export ATSHOMERELOC=ATS-0.2.10
		export PATH=$PATH:$ATSHOME/bin

#. Configure 

	.. attention:: You may need to install ``autoconf`` package first

	.. code-block:: bash

		cd ~/ats
		aclocal
		autoconf
		./configure

#. Make 

	.. code-block:: bash

		make all

#. Make sure that all the binaries are under ``bin``, and all the libraries are under ``ccomp/lib`` and ``ccomp/lib64``.


Next, we are building ATS 2. CMake 2.8+ is recommended.


#. Download source code from GitHub, https://github.com/githwxi/ATS-Postiats/archive/master.zip
#. Unzip it into a folder, e.g. ``~/ats2``
#. Setting up environment variables

	.. code-block:: bash

		export ATSHOME=~/ats
		export ATSHOMERELOC=ATS-0.2.10
		export PATSHOME=~/ats2
		export PATH=$PATH:$ATSHOME/bin:$PATSHOME/bin

#. Make

	.. code-block:: bash

		cd ~/ats2/src/BUILD
		cmake ..
		make

		mkdir ~/ats2/bin
		cp patsopt ~/ats2/bin/


Next, build libraries and tools

#. Generate source code from templates

	.. code-block:: bash

		cd ~/ats2
		make -f codegen/Makefile_atslib
		make -f codegen/Makefile_atscntrib

#. Make C Target Compiler and Libraries

	.. code-block:: bash

		cd ~/ats2/ccomp
		make

#. Make utilities

	.. code-block:: bash

		cd ~/ats2/libatsyntax
		make

		cd ~/ats2/utils/atscc
		make
		cp patscc ~/ats2/bin/

		cd ~/ats2/utils/atsyntax
		make