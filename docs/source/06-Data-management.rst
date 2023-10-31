Data-management
===============

Overview
--------

Data Managers are responsible for:

1. Initially bringing study data requested by the user into SRCP
2. Creating folders within the project and setting permissions for the
   study data
3. Moving data between the “upload” and “download” triage folders and a
   user’s project folder (e.g. bringing code in or results out)
4. Checking data/code that is brought in or out of SRCP to make sure it
   does not contain anything it shouldn’t

Prerequisites
-------------

To perform the data management tasks, the Data Manager needs to:

1. Understand how to `log into
   SRCP <https://github.com/epi-analysis/SRCP/wiki/00-Logging-in-for-the-First-Time>`__
2. Be able to start a `remote desktop session on
   SRCP <https://github.com/epi-analysis/SRCP/wiki/01-Getting-Started#interactive-apps---remote-desktop-session>`__
3. Set up an `SFTP
   client <https://github.com/epi-analysis/SRCP/wiki/04-Taking-files-on-and-off-SRCP#sftp-clients>`__

Bringing study data into SRCP
-----------------------------

As summary of the process for bringing study data into SRCP is:

1. Set up the SFTP connection to SRCP
2. Navigate to the “upload” triage folder and upload the files
3. Log in to the SRCP web interface
4. Start a remote desktop session
5. Move the files from your “upload” triage folder to the required
   project folder
6. Confirm that an analysis folder has been set up and permissions are
   set correctly in the project
7. Notify the user
8. Tidy up

Prerequisite - setting up the project folder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before bringing in the data, it is recommended that some additional
subfolders are created in the project folder
(e.g. ``2023_06_20_Smith_ENDR023_2020``). The project folder can be
written to by members of the ``platform-b864dfnfpqj-managers`` group,
i.e. Data Managers, but users cannot write to this folder. Users will
need a location to do their work and save results - the ``analysis``
subfolder. The data should be stored in a read-only location so that it
cannot be changed accidentally - the ``data`` subfolder. The suggested
folder structure looks like this:

::

   ├── 2023_06_20_Smith_ENDR023_2020
   │   ├── data
   │   │   ├── subfolders in data folder
   │   └── analysis

The user needs permission to **read, write and execute** in the
``analysis`` folder. The best way to achieve this is with this command:

``nfs4_setfacl -a "A:fdg:project-<project-id>-users@hpc.cam.ac.uk:RWX" /srv/projects/<userproject>/analysis``

**TO DO - make this command (and others) available in the shared folder
for easy cut and paste**

where <project-id> is the 11 character alphanumeric identifier
(e.g. ck5gh6d3se) and <userproject> is the folder name
(e.g. ``2023_06_20_Smith_ENDR023_2020``). **TIP** If you list the
project folder contents (``ls -l``) the <project-id> is available for
copying and pasting:

.. raw:: html

   <p align="center">

.. raw:: html

   </p>

We also need to remove the permissions for “other” users:
``chmod o-rwx /srv/projects/<userproject>/analysis``

The user needs permission to **read and execute** in the ``data`` folder
(and subfolders) and **read** files - they should not be able to write
to this location to avoid inadvertent changes being made to the data.
The best way to achieve this is with these commands, **noting the ``RX``
permission for directories and ``R`` permission for files this time**:

::

   nfs4_setfacl -a "A:gd:project-<project-id>-users@hpc.cam.ac.uk:RX" /srv/projects/<userproject>/data
   nfs4_setfacl -a "A:gf:project-<project-id>-users@hpc.cam.ac.uk:R" /srv/projects/<userproject>/data

**TO DO - make this command (and others) available in the shared folder
for easy cut and paste**

Example of uploading a data release using WinSCP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1.  Connect to the Cambridge VPN or use a computer connected to the
    Cambridge network

2.  Start WinSCP and where you will be presented with the Login
    dialogue. Select the session for SRCP that you (saved
    previously)[https://github.com/epi-analysis/SRCP/wiki/04-Taking-files-on-and-off-SRCP#example-of-setting-up-winscp],
    or enter the details if you have not already done this -
    **data-epi-analysis.srcp.hpc.cam.ac.uk** on port 22 and your CRSid
    as the username (i.e. the same username you use to log into the SRCP
    web interface).

    .. raw:: html

       <p align="center">

    .. raw:: html

       </p>

3.  Click the Login button.

4.  Enter your CRS/Raven password (the same as for the SRCP web
    interface) and then enter a TOTP from your mobile device for 2
    factor authentication (the same as for the SRCP web interface)

    .. raw:: html

       <p align="center">

    .. raw:: html

       </p>

5.  You should now be connected. The triage upload and download folders
    on SRCP are shown on the right, and your local machine’s folders on
    the left. You can transfer files between these locations.

    .. raw:: html

       <p align="center">

    .. raw:: html

       </p>

6.  Locate the data release on your local machine (left side) that you
    wish to upload. Drag and drop it into the upload folder on SRCP
    (right side)

    .. raw:: html

       <p align="center">

    .. raw:: html

       </p>

7.  Switch to a browser, log into SRCP and `start a remote desktop
    session <https://github.com/epi-analysis/SRCP/wiki/01-Getting-Started#interactive-apps---remote-desktop-session>`__.
    Currently we are using Account = tq7cr8nq6x7 and Partition =
    tq7cr8nq6x7-cpu

8.  Copy the data from your ``triage/<yourusername>/upload`` folder to
    the user’s project ``data`` subfolder:

    1. On the command line:
       ``$ cp /srv/data-manager/triage/<yourusername>/upload/<filename> /srv/projects/<userproject>/data``
    2. Or from the file manager application (which works in a similar
       way to Windows File Explorer)

9.  If required, a ``7z`` archive can be unzipped: ``7zG x myfile.7z``

10. We finally need to remove recursively the read and execute
    permission for “other” users:
    ``chmod -R o-rwx /srv/projects/<userproject>/data``

11. If the data are large and a copy is stored elsewhere, delete any
    copies of the data from your triage folder to save storage space.

Process for users wishing to bring files into SRCP
--------------------------------------------------

Users may ask Data Managers to allow them to upload files to SRCP. This
might be to bring in extra data sets or bespoke code that they cannot
download from the standard repositories available in SRCP.

A summary of the process for users wishing to bring supplementary data
or code into SRCP is:

1. The user connects to their “upload” triage folder using SFTP and
   uploads the files.
2. The user notifies a Data Manager (datasharing@mrc-epid.cam.ac.uk) of
   the file names. These should be in the user’s “upload” triage folder
   - the user should have followed the steps for `uploading a file via
   STFP. <https://github.com/epi-analysis/SRCP/wiki/04-Taking-files-on-and-off-SRCP#example-of-uploading-files-using-winscp>`__
3. The Data Manager copies the files to their “download” triage folder
   on SRCP
4. The Data Manager connects to SRCP via SFTP and downloads the files to
   their local machine
5. The Data Manager inspects the files and confirms that they contain
   appropriate data/code
6. On SRCP, the Data Manager moves the files from the user’s “upload”
   triage folder to the user’s project folder and notifies the user
7. The user uses the files that are now available in their project
   folder
8. Tidy up

Example of enabling a user to bring files into SRCP using WinSCP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. After receiving a request to make a user’s uploaded files available,
   you will need to download the files yourself to check them. The
   initial step is to copy the files from the user’s “upload” folder to
   your own “download” folder.

2. To do this, log into SRCP and `start a remote desktop
   session <https://github.com/epi-analysis/SRCP/wiki/01-Getting-Started#interactive-apps---remote-desktop-session>`__.
   Currently we are using Account = tq7cr8nq6x7 and Partition =
   tq7cr8nq6x7-cpu

3. Navigate to the user’s triage folder
   ``/srv/data-manager/triage/<username>/upload`` either on the command
   line or in File Manager

4. Copy the files from the user’s triage folder
   ``/srv/data-manager/triage/<username>/upload`` to your own download
   triage folder ``/srv/data-manager/triage/<yourusername>/download``
   either on the command line or in File Manager.

5. Start WinSCP and log in using the details (saved
   previously)[https://github.com/epi-analysis/SRCP/wiki/04-Taking-files-on-and-off-SRCP#example-of-setting-up-winscp].
   Navigate to your download folder and copy the files to a location
   accessible from your local machine.

.. raw:: html

   <p align="center">

.. raw:: html

   </p>

6. Inspect the files. **TO CONFIRM** If they contains data confirm that
   the user has permission to use it (because we don’t want to be seen
   to enable analyses on data that is not being used correctly). If they
   are Singularity containers (.sif), run a scanner on them.

7. If the files are OK then on SRCP, move the files from the user’s
   “upload” triage folder to the user’s project (analysis) folder either
   on the command line or in File Manager. Notify the user that the
   files are ready for use.

8. (If the files are large then delete them from both your own and the
   user’s triage folder to save space? Assume user has a back up on
   their local computer?)

Process for users wishing to take files off SRCP
------------------------------------------------

Users will ask Data Managers to allow them to download files from SRCP.
This is so that they can remove summary results for their research, not
for removing data from SRCP.

A summary of the process for users wishing to download files from SRCP
is:

1. The user moves the files to their “download” triage folder on SRCP
2. The user notifies a Data Manager (datasharing@mrc-epid.cam.ac.uk) of
   the file names they wish to download and their location.
3. The Data Manager copies the files to their “download” triage folder
   on SRCP
4. The Data Manager connects to SRCP via SFTP and downloads the files to
   their local machine
5. The Data Manager inspects the files and confirms that they meet the
   Disclosure Control Rules:

-  provide a description of what the file contains, how it was generated
   and its relevance to the research question
-  files should only contain aggregated, summary results
-  results are clearly labelled
-  files should not have any participant or sample IDs
-  mask phenotype counts lower than 5 (e.g. if the results show 3 people
   have lung cancer, this should be masked)

7. On SRCP, the Data Manager moves the files to the user’s “download”
   triage folder and notifies the user
8. The user connects to their “download” triage folder using SFTP and
   `downloads the
   files <https://github.com/epi-analysis/SRCP/wiki/04-Taking-files-on-and-off-SRCP#example-of-downloading-files-using-winscp>`__

Example of enabling a user to download files from SRCP using WinSCP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. After receiving a request from a user to make some of their files
   available for download, you will need to download the files yourself
   to check them. The initial step is to copy the files from the
   location specified by the user (e.g. the analysis subfolder in their
   project folder) to your own “download” folder.

2. To do this, log into SRCP and `start a remote desktop
   session <https://github.com/epi-analysis/SRCP/wiki/01-Getting-Started#interactive-apps---remote-desktop-session>`__.
   Currently we are using Account = tq7cr8nq6x7 and Partition =
   tq7cr8nq6x7-cpu

3. Navigate to the location specified by the user (e.g. the analysis
   subfolder in their project folder) either on the command line or in
   File Manager

4. Copy the files from the location specified by the user to your own
   download triage folder
   ``/srv/data-manager/triage/<yourusername>/download`` either on the
   command line or in File Manager.

5. Start WinSCP and log in using the details (saved
   previously)[https://github.com/epi-analysis/SRCP/wiki/04-Taking-files-on-and-off-SRCP#example-of-setting-up-winscp].
   Navigate to your download folder and copy the files to a location
   accessible from your local machine.

.. raw:: html

   <p align="center">

.. raw:: html

   </p>

6. Inspect the files. **TO CONFIRM** The files need to be checked to
   ensure that they do not contain study data, only summary results.
   More detailed guidance can be found
   `here <https://ukdataservice.ac.uk/app/uploads/thf_datareport_aw_web.pdf>`__.
   This guidance is very detailed, so a balance needs to be struck
   around what level of checking is needed.

7. If the files are OK then on SRCP, move the files from the the
   location specified by the user to the user’s “download” triage folder
   ``/srv/data-manager/triage/<yourusername>/download`` either on the
   command line or in File Manager. Notify the user that the files are
   ready for download.

8. (If the files are large then delete them from both your own and the
   user’s triage folder to save space? Confirm with the user that they
   have downloaded the files to their local computer?)

Work in progress
----------------

Using the command line
~~~~~~~~~~~~~~~~~~~~~~

Once the remote desktop session is running, the following steps can be
followed from a terminal:

**Download** 1. Navigate to the folder specified by the user:
``$ cd /<foldername>`` 2. Look in the folder ``$ ls -la`` 3. Copy the
file requested by the user to your own triage download folder:
``$ cp <filename> /srv/data-manager/triage/<yourusername>/download`` 4.
Connect via SFTP and download the file 5. Check the file for individual
level data (i.e. the data should be results only *a more rigorous
checklist may be developed*) 6. If the file looks OK, copy the file to
the user’s triage download location
``$ cp <filename> /srv/data-manager/triage/<username>/download`` 7.
Either notify the user that the file was moved as requested to their
triage download folder and is available via SFTP, or explain what needs
to be changed for the file to be acceptable for download.

**Upload** 1. Navigate to the user’s triage folder:
``$ cd /srv/data-manager/triage/<username>/upload`` where ``<username>``
is the CRSid of the user 2. Look in the folder ``$ ls -la`` 3. Copy the
file requested by the user to your own triage download folder 4. Connect
via SFTP and download the file to your local computer 5. Check the file
for **what - malicious code? data that they shouldn’t have - how do we
know?** 6. If the file looks OK, copy the file requested by the user to
the location required (for example, the user’s project folder)
``$ cp /srv/data-manager/triage/<username>/upload/<filename> /srv/projects/<projectname>``
where ``<projectname>`` is the user’s project 7. Either notify the user
that the file was moved and tell them the location, or explain what
needs to be changed for the file to be acceptable for upload.

Using file manager
~~~~~~~~~~~~~~~~~~

Once the remote desktop session is running, the following steps can be
followed using the file manager application:

**Download** 1. Navigate to the folder specified by the user 2. Look in
the folder 3. Copy the file requested by the user to your own triage
download folder (``/srv/data-manager/triage/<yourusername>/download``)
4. Connect via SFTP and download the file 5. Check the file for
individual level data (i.e. the data should be results only *a more
rigorous checklist may be developed*) 6. If the file looks OK, copy the
file to the user’s triage download location
(``/srv/data-manager/triage/<username>/download`` where ``<username>``
is the CRSid of the user) 7. Either notify the user that the file was
moved as requested to their triage download folder and is available via
SFTP, or explain what needs to be changed for the file to be acceptable
for download.

**Upload** 1. Navigate to the user’s triage folder:
``/srv/data-manager/triage/<username>/upload`` where ``<username>`` is
the CRSid of the user 2. Look in the folder 3. Copy the file requested
by the user to your own triage download folder 4. Connect via SFTP and
download the file to your local computer 5. Check the file for **what -
malicious code? data that they shouldn’t have - how do we know?** 6. If
the file looks OK, copy the file requested by the user to the location
required (for example, the user’s project folder)
``/srv/projects/<projectname>`` where ``<projectname>`` is the user’s
project 7. Either notify the user that the file was moved and tell them
the location, or explain what needs to be changed for the file to be
acceptable for upload.

Examining items to be taken in or out
-------------------------------------

Files that are to be taken out from the system should be checked to
ensure that they do not contain study data, only summary results. More
detailed guidance can be found
`here <https://ukdataservice.ac.uk/app/uploads/thf_datareport_aw_web.pdf>`__
and `here <https://re-docs.genomicsengland.co.uk/airlock_rules/#>`__.
This guidance is very detailed, so a balance needs to be struck around
what level of checking is needed.

A standard check might be to look for participant IDs in the data export
as this is clearly an indicator of individual level data.

Often a more formal process is used where researchers have to submit a
form with details about what the results are and how they relate to the
project. There can be a service level agreement for the time taken to
review requests.

For data that is to be brought in, checks should be made about whether
the user has permission to use this data and move it to different
locations. Some data sets might not be a concern, for example publicly
available data on air pollution. Questions should be raised if a user is
trying to bring in something sensitive like patient records.

Users may want to bring in code or containers. This should be scanned
(TO DO - recommend some tools) to check for security problems.

Notes on project permissions
----------------------------

The platform manager group can rwx on folders and files created in
project folders by any other platform - controlled by NFS ACL. The
children of the project folder inherit the permissions.

When the platform manager creates the data/analysis folders, they apply
ACL permissions to these which are inherited by the items created in
these folders.
