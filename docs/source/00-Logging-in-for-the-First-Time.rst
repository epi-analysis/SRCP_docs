In order to connect to SRCP, you will need the following things:

-  CRSid and associated password (AKA Raven password), which should have
   been provided as part of the Visiting Workers process
-  Connection to the Cambridge University VPN (instructions
   `here <https://help.uis.cam.ac.uk/service/network-services/remote-access/uis-vpn>`__)
-  Complete the `SRCP User Access
   Request <https://www.hpc.cam.ac.uk/srcp-request-user-access>`__ - you
   will be asked to “Log in with Raven” if not connected to the VPN, use
   your CRSid and password.
-  To complete the access request form you will also need the following
   information:

   -  SRCP platform type = vHPC
   -  User’s vHPC Level of Access = Project User
   -  Project Unique ID = will be provided by the data management team

-  The address of the epi-analysis SRCP platform:
   `epi-analysis.srcp.hpc.cam.ac.uk <https://epi-analysis.srcp.hpc.cam.ac.uk/>`__
   - **you will need to be connected to the Cambridge VPN**
-  A mobile device to set up for two factor authentication

If you need help with any of this information, please contact `Tom
Bishop <mailto:trpb2@cam.ac.uk>`__

Configuring Two Factor Authentication
-------------------------------------

SRCP uses two factor authentication. The first time log in is attempted
by going to
`epi-analysis.srcp.hpc.cam.ac.uk <https://epi-analysis.srcp.hpc.cam.ac.uk/>`__,
the following steps are needed:

-  Install the Two Factor Authentication application
-  Retrieve the Token
-  Configure the Application

Preparing Your Phone for Two Factor Authentication
--------------------------------------------------

There are several steps needed to configure your phone for use with
SRCP.

Securing Your Phone
~~~~~~~~~~~~~~~~~~~

Information on securing your device is in the `SRCPS User Security
Policy <https://docs.hpc.cam.ac.uk/srcp/isms-docs/security-policy.html#security-policy>`__.
Please ensure this has been read and understood this before proceeding
with configuring two factor authentication access.

Installing a Two Factor Authentication Application
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An application is needed to generate the one time login tokens which
enable access to SRCP.

We support several mobile applications for both Android and iPhone:

+-----------------------------+-----------------+----------------------+
| Application                 | iPhone          | Android              |
+=============================+=================+======================+
| FreeOTP                     | `Yes            | `Yes <https://play.g |
|                             | <https://itunes | oogle.com/store/apps |
|                             | .apple.com/gb/a | /details?id=org.fedo |
|                             | pp/freeotp-auth | rahosted.freeotp>`__ |
|                             | enticator/id872 |                      |
|                             | 559395?mt=8>`__ |                      |
+-----------------------------+-----------------+----------------------+
| Google Authenticator        | `Yes            | `Ye                  |
|                             |  <https://itune | s <https://play.goog |
|                             | s.apple.com/gb/ | le.com/store/apps/de |
|                             | app/google-auth | tails?id=com.google. |
|                             | enticator/id388 | android.apps.authent |
|                             | 497605?mt=8>`__ | icator2&hl=en_GB>`__ |
+-----------------------------+-----------------+----------------------+

Retrieving Your Token
---------------------

Adding a Token to a Mobile Phone
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Connect to the Cambridge University VPN and go to the `login
page <https://epi-analysis.srcp.hpc.cam.ac.uk/>`__

Upon browsing to this page the user will be presented with a login page:

.. raw:: html

   <p align="center">

.. raw:: html

   </p>

Here the user should enter their credentials to proceed - the CRSid and
Raven password.

If this is the first time theuser has attempted to in they will be
presented with a prompt to configure Two Factor Authentication. It will
look similar to the image shown below.

.. raw:: html

   <p align="center">

.. raw:: html

   </p>

The page has a barcode on it, which can be scanned by a Two Factor
Authentication management application. There is a video below showing
this process for an android handset:

|android|

Recovering from a lost token or device
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If a user loses their Time-based one-time password (TOTP) codes or
mobile device, they will be unable to access the platform until they
have raised a support request with the SRCP Support Team, who at that
point are the only people who can regenerate the user’s TOTP codes.
Before doing this however, the SRCP Support Team must go through a
process to establish the real identity of this user. This involves
confirming the reset with the MRC Epidemiology Unit team.

If you have lost your mobile device or token please submit a support
request to the `SRCP helpdesk <mailto:support@hpc.cam.ac.uk>`__. The
user must also notify the MRC Epidemiology Unit team with whom the SRCP
helpdesk contacts for approval. This must happen before the SRCP
helpdesk can issue a replacement token.

Once the MRC Epidemiology Unit has approved the token reset request and
the user has demonstrated ownership of their password the Helpdesk will
issue a new private token.

.. |android| image:: https://user-images.githubusercontent.com/8521654/234272219-f6e9bbb7-4e54-44b3-b1cd-f1f4bfd3d8de.png
   :target: https://player.vimeo.com/video/374700786
