Running Jobs on SRCP
--------------------

SLURM is an open source workload management and job scheduling system
used by SRCP. SLURM is normally used from the command line, therefore to
get started you will **need to have a remote desktop session running**.
Jobs are submitted to SLURM via scripts.

Sample submission scripts
-------------------------

In normal use of SLURM, one creates a batch job which is a shell script
containing the set of commands to run, plus the resource requirements
for the job which are coded as specially formatted shell comments at the
top of the script. A job script can be resubmitted with different
parameters (e.g. different sets of data or variables).

A read-only sample submission script with parameters set up for your
project can be found in your project folder in the file called
``slurm_submit.template``.

Lines beginning ``#SBATCH`` are directives to the batch system. The rest
of each directive specifies arguments to the ``sbatch`` command. SLURM
stops reading directives at the first executable (i.e. non-blank, and
doesn’t begin with #) line.

The first directives should not be changed as they are set up for your
project:

::

   #! Which project should be charged:
   #SBATCH -A projectID
   #! Which partition/cluster am I using?
   #SBATCH -p projectID-cpu

Editing the script
~~~~~~~~~~~~~~~~~~

Make a copy of the sample script, and edit it using the VIM editor
(``$ vim``). For help using vim see this
`guide <https://www.linuxfoundation.org/blog/blog/classic-sysadmin-vim-101-a-beginners-guide-to-vim>`__

Set up
~~~~~~

The main directives to modify are:

::

   #! Name of the job:
   #SBATCH -J cpujob
   #! How many whole nodes should be allocated?
   #SBATCH --nodes=1
   #! How many (MPI) tasks will there be in total?
   #SBATCH --ntasks=1
   #! How much wallclock time will be required?
   #SBATCH --time=00:10:00
   #! What types of email messages do you wish to receive?
   #SBATCH --mail-type=FAIL
   #! Uncomment this to prevent the job from being requeued (e.g. if
   #! interrupted by node failure or system downtime):
   ##SBATCH --no-requeue

The ``--time`` parameter needs to be set to a value sufficiently high
for your code to finish running.

The ``--nodes`` parameter will usually be set to 1.

Modules
~~~~~~~

The following section should be modified to specify the modules that are
needed to run your code:

::

   #! Optionally modify the environment seen by the application
   #! (note that SLURM reproduces the environment at submission irrespective of ~/.bashrc):
   . /etc/profile.d/software.sh               # Leave this line (enables the module command)
   module purge                               # Removes all modules still loaded
   #module load python/3.9.12/gcc r/4.1.3/gcc # Load additional modules

Executable and code
~~~~~~~~~~~~~~~~~~~

The executable and code to run are specified like this:

::

   #! Full path to application executable: 
   application="python3 test.py"

For an example script called ``test.py`` run from Python.

Output
~~~~~~

The following statement can be modified to store any outputs from the
job:

::

   #! Work directory (i.e. where the job will run):
   workdir="$SLURM_SUBMIT_DIR"  # The value of SLURM_SUBMIT_DIR sets workdir to the directory
                                # in which sbatch is run.

Submitting the job to the queuing system
----------------------------------------

From the command line in your remote desktop session, the command sbatch
is used to submit jobs, e.g.

::

   sbatch submission_script

The command will return a unique job identifier, which is used to query
and control the job and to identify output. See the man page (*man
sbatch*) for more options.

Deleting jobs
-------------

To cancel a job (either running or still queuing) use scancel:

::

   scancel <jobid>

The ``<jobid>`` is printed when the job is submitted, alternatively use
the commands ``squeue``, ``qstat`` or ``showq`` to obtain the job ID.
