.. SafeNet Trusted Access documentation master file, created by
   sphinx-quickstart on Mon Mar 22 11:01:57 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

====================================================================
Azure Conditional Authentication Factors with SafeNet Trusted Access
====================================================================

.. toctree::
   :maxdepth: 3
   :hidden:
   :caption: Contents:

   index

Overview
========

Azure Conditional Authentication Factors (Custom Controls) allows extending the Azure Active Directory authentication with a third party authentication provider, using OIDC protocol.
When using custom controls, the users are redirected to SafeNet Trusted Access to satisfy authentication requirements outside of Azure Active Directory. To satisfy this control, a user's browser is redirected to SafeNet Trusted Access, performs any required authentication, and is then redirected back to Azure Active Directory. Azure Active Directory verifies the response and, if the user was successfully authenticated or validated, the user continues in the Conditional Access flow.

.. blockdiag::

    blockdiag azure {

      node_width=350;
      node_height=200;
      default_fontsize = 35;
      span_height = 60;


      A [label = "Azure\n Active Directory"];
      B [label = "AAD Username"];
      C [label = "AAD Password"];
      D [label = "STA Authentication"];

      A -> B -> C -> D -> A;

    }


.. note:: For more information about Microsoft Conditional Authentication Factors (Custom Controls), please visit https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/controls


Prerequisites
=============

  - Existing Azure Active Directory domain with **Premium P1 subscription** - (**P1** or above is required for Conditional Access)
  - Test User synchronized to both AAD and STA - (matching UPN)

Configuration Steps
===================

The configuration requires the following steps:

  **In STA**

  - Add **Azure Conditional Authentication Factor** application in STA
  - Copy the generated **JSON** code
  - Assign the application to users
  - Configure STA Authentication Policy

  **In Azure**

  - Create **Custom Control** using the provided **JSON** code
  - Create **Conditional Access** policy to use the new **Custom Control**


SafeNet Trusted Access
======================

Create new Azure Conditional Authentication Factors Application
***************************************************************

In the STA Console create a new application by following these steps:

	- Go to the :guilabel:`Applications` tab
 	- Click :guilabel:`+` and search for **Azure Conditional Authentication Factors**
  - Rename the Application to a desired application name
  - Click :guilabel:`Add` to add the application to your library

The application is added:

.. thumbnail:: _images/aad_add.png
    :align: center
