Explanation of file transfers on SRCP
-------------------------------------

An important feature of the SRCP Platform is the strict control and
auditing over the upload and download of files. Users cannot access
their project folder from outside SRCP. This prevents data from being
removed from or brought onto the system without permission. Before any
file is released from the system, it is checked by a Data Manager to
ensure that it meets the **Disclosure Control Rules**:

-  provide a description of what the file contains, how it was generated
   and its relevance to the research question
-  files should only contain aggregated, summary results
-  results are clearly labelled
-  files should not have any participant or sample IDs
-  mask phenotype counts lower than 5 (e.g. if the results show 3 people
   have lung cancer, this should be masked)

Data brought onto the system should be cleared for use on the research
question. Code that is being brought in should be sourced from a
reputable location so that it does not contain malware. In SRCP the
transfer process is managed by using a triage location for each user
that is only accessible to the user from outside SRCP. They can use SFTP
to transfer files to and from the triage location. Only a Data Manager
can move files between a user’s project folder and the triage folder
after inspecting them. It is the responsibility of the users to notify a
Data Manager that files are awaiting approval so they can authorise and
move them. Once the move is complete, the files are available to the
user immediately.

.. raw:: html

   <p align="center">

.. raw:: html

   </p>

Process for downloading files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. A user wishes to download some results from SRCP
2. They notify a Data Manager (datasharing@mrc-epid.cam.ac.uk) of the
   file name, location (e.g. their project folder) and a statement of
   how it meets the Disclosure Control Rules (see above)
3. The Data Manager inspects the file and confirms that it contains
   results, not any individual level data
4. The Data Manager moves the file from the user’s project folder to
   their “download” triage folder and notifies the user
5. The user connects to their “download” triage folder using SFTP and
   downloads the file

Process for uploading files
~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. A user wishes to upload some supplementary data to SRCP
2. The user connects to their “upload” triage folder using SFTP and
   uploads the file
3. They notify a Data Manager (datasharing@mrc-epid.cam.ac.uk) of the
   file name, location (their “upload” triage folder) and a statement
   that permission has been granted for the data to be used in this
   research (data) or that the code is from a reputable source (code)
4. The Data Manager inspects the file and confirms that it contains
   appropriate data/code
5. The Data Manager moves the file from the user’s “upload” triage
   folder to the user’s project folder and notifies the user
6. The user uses the file that is now available in their project folder

Connecting to epi-analysis SRCP with SFTP
-----------------------------------------

The **address** of the epi-analysis SFTP site is
`data-epi-analysis.srcp.hpc.cam.ac.uk <data-epi-analysis.srcp.hpc.cam.ac.uk>`__.

The **username**, **password** and **2 factor authentication device**
are the same as those used to log into the web interface.

SFTP Clients
~~~~~~~~~~~~

To connect, an `SFTP client <https://www.sftp.net/clients>`__ is
required such as:

-  `FileZilla <https://filezilla-project.org>`__
-  `WinSCP <https://winscp.net>`__
-  `CyberDuck <https://cyberduck.io>`__
-  `rsync <https://linux.die.net/man/1/rsync>`__
-  `sftp <https://linux.die.net/man/1/sftp>`__

Example of setting up WinSCP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Connect to the Cambridge VPN

2. Start WinSCPand where you will be presented with the Login dialogue

   .. raw:: html

      <p align="center">

   .. raw:: html

      </p>

3. Choose SFTP as the protocol, enter the hostname as
   **data-epi-analysis.srcp.hpc.cam.ac.uk**, set the port to 22 and
   enter your CRSid as the username (i.e. the same username you use to
   log into the SRCP web interface).

   .. raw:: html

      <p align="center">

   .. raw:: html

      </p>

4. Click Save and then click OK to save the session as a site. This will
   allow you to reconnected more easily in the future.

Example of uploading files using WinSCP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Connect to the Cambridge VPN

2. Start WinSCPand where you will be presented with the Login dialogue.
   Select the session for SRCP that you saved previously

   .. raw:: html

      <p align="center">

   .. raw:: html

      </p>

3. Click the Login button.

4. Enter your CRS/Raven password (the same as for the SRCP web
   interface) and then enter a TOTP from your mobile device for 2 factor
   authentication (the same as for the SRCP web interface)

   .. raw:: html

      <p align="center">

   .. raw:: html

      </p>

5. You should now be connected. The triage upload and download folders
   on SRCP are shown on the right, and your local machine’s folders on
   the left. You can transfer files between these locations.

   .. raw:: html

      <p align="center">

   .. raw:: html

      </p>

6. Locate the file on your local machine (left side) that you wish to
   upload. Drag and drop it into the upload folder on SRCP (right side)

   .. raw:: html

      <p align="center">

   .. raw:: html

      </p>

7. Contact a Data Manager (datasharing@mrc-epid.cam.ac.uk) and let them
   know that you need files moved from your “upload” folder to your
   project folder. They will check the files, move them to your project
   folder if all is OK and notify you that the files are available or
   advise what changes are needed.

Example of downloading files using WinSCP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

0. **TO DO - make sure permissions are set so that DM can read the
   file**

1. Contact a Data Manager (datasharing@mrc-epid.cam.ac.uk) and let them
   know that you need files moved from your project folder to your
   “download” folder. They will check the files, move them to your
   download folder if all is OK and notify you that they are available
   for download or advise what changes are needed.

2. When you have received notification from the Data Manager that the
   files are ready for you to download, connect to the Cambridge VPN.

3. Start WinSCPand where you will be presented with the Login dialogue.
   Select the session for SRCP that you saved previously

   .. raw:: html

      <p align="center">

   .. raw:: html

      </p>

4. Click the Login button.

5. Enter your CRS/Raven password (the same as for the SRCP web
   interface) and then enter a TOTP from your mobile device for 2 factor
   authentication (the same as for the SRCP web interface)

   .. raw:: html

      <p align="center">

   .. raw:: html

      </p>

6. You should now be connected. The triage upload and download folders
   on SRCP are shown on the right, and your local machine’s folders on
   the left. You can transfer files between these locations.

   .. raw:: html

      <p align="center">

   .. raw:: html

      </p>

7. Locate the file on SRCP (right side) that you wish to download. Drag
   and drop it to the required folder on your local machine (left side)

   .. raw:: html

      <p align="center">

   .. raw:: html

      </p>