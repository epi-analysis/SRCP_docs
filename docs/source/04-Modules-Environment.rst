Modules Environment
===================
Modules
-------

Software on SRCP is primarily controlled through the *modules* environment. By loading and switching modules you control the compilers, libraries and software available.

When compiling or running programs on SRCP you will need to set up the correct modules, to load your compiler and any libraries that are required (e.g. numerical libraries, IO format libraries).

Basic usage of the ``module`` command on SRCP is covered below. For full documentation please see:

`Linux manual page on modules <http://linux.die.net/man/1/module>`__

Information on the available modules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Finding out which modules (and hence which compilers, libraries and software) are available on the system is performed using the ``module avail`` command:

::

   [user@system ~]$ module avail

This will list all the names and versions of the modules available on the service. Not all of them may work for your account however, due to, for example, licencing restrictions. You will notice that for many modules we have more than one version, each of which is identified by a version number. One of these versions is the default. As the service develops the default version will change.

How to search for modules
~~~~~~~~~~~~~~~~~~~~~~~~~

The ``keyword`` command can be used to search for specific items in the available modules:

::

   #The below command will list all available modules with the phrase 'python-3.6' in them
   [user@system ~]$ module keyword python-3.6
   python-3.6.1-gcc-5.4.0-23fr5u4
   python-3.6.1-gcc-5.4.0-64u3a4w
   python-3.6.1-gcc-5.4.0-vag3zpv
   python-3.6.1-gcc-5.4.0-xk7ym4l
   python-3.6.2-gcc-5.4.0-me5fsee
   python-3.6.2-intel-17.0.4-lv2lxsb

Identifying currently loaded modules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The simple ``module list`` command will give the names of the modules and their versions you have presently loaded in your envionment:

::

   [user@login-e-11 ~]$ module list
   Currently Loaded Modulefiles:
   1) slurm                          6) turbovnc/2.0.1                11) intel/impi/2017.4/intel       16) intel/bundles/complib/2017.4
   2) rhel7/global                   7) vgl/2.5.1/64                  12) intel/libs/idb/2017.4         17) rhel7/default-peta4
   3) spack/current                  8) singularity/current           13) intel/libs/tbb/2017.4
   4) dot                            9) intel/compilers/2017.4        14) intel/libs/ipp/2017.4
   5) java/jdk1.8.0_45              10) intel/mkl/2017.4              15) intel/libs/daal/2017.4

Loading, unloading and swapping modules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To load a module to use ``module add`` or ``module load``. For example, to load the pgi commpiler into the development environment:

::

   module load pgi

This will load the default version of the pgi compilers Library. If you need a specfic version of the module, you can add more information:

::

   module load pgi/2018

will load version 18.1 for you, regardless of the default. If you want to clean up, ``module remove`` will remove a loaded module:

::

   module remove pgi

(or ``module rm pgi`` or ``module unload pgi``) will unload whatever version of pgi (even if it is not the default) you might have loaded.
