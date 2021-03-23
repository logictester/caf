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

  **In :abbr:`STA (SafeNet Trusted Access)`**

  - Add **Azure Conditional Authentication Factors** application in STA
  - Copy the generated :ref:`JSON <JSON>` code
  - Assign the application to users
  - `Configure STA Authentication Policy`_

  **In Azure**

  - Create **Custom Control** using the provided **JSON** code
  - Create **Conditional Access** policy to use the new **Custom Control**


SafeNet Trusted Access configuration
====================================

Open SafeNet Trusted Access Console (you can use the following links based on your availability zone, opens in a new tab)

|US Zone|

.. |US Zone| raw:: html

   <a href="https://sta.us.safenetid.com" target="_blank">US Zone SafeNet Trusted Access Console</a>

|EU Zone|

.. |EU Zone| raw:: html

   <a href="https://sta.eu.safenetid.com" target="_blank">EU Zone SafeNet Trusted Access Console</a>

|Classic Zone|

.. |Classic Zone| raw:: html

   <a href="https://sta.safenetid.com" target="_blank">Classic Zone SafeNet Trusted Access Console</a>


Create new Azure Conditional Authentication Factors Application
***************************************************************

In the STA Console create a new application by following these steps:

  - Go to the :guilabel:`Applications` tab

  - Click :guilabel:`+` and search for **Azure Conditional Authentication Factors**, click it to select

  - *(Optional)* Rename the Application to a desired application name

  - Click :guilabel:`Add` to add the application to your library

.. _JSON:

The application is added and **JSON** code is generated:

.. thumbnail:: _images/aad_add.png
    :align: center

Click :guilabel:`Copy` to copy the **JSON** code or :guilabel:`Email` to open a new email with **JSON** code pasted in and ready to send

Click :guilabel:`Assign` to assign the created application to the required users

.. thumbnail:: _images/assign.png

Click :guilabel:`Save Configuration` to save the application


_`Configure STA Authentication Policy`
**************************************

In the STA Console, create a new Access Policy for Azure Conditional Authentication Factors application by following these steps:

  - Go to the :guilabel:`Policies` tab

  - Click :guilabel:`+` to add a new Policy

  - Name the new Policy, *for example Azure Custom Control*

  - **Polcy Scope**

    - Under **Users**, click :guilabel:`All Users` to apply to all users or :guilabel:`Any of these User Groups:` to apply to specifc User Groups

    - Under **Applications**, click :guilabel:`Any of these Applications`, click in the field and select **Azure Conditional Authentication Factors** application

  - **Default Requirements**

    - Select the desired authentication method *for example* :guilabel:`Token Based Authentication (OTP)` and :guilabel:`Every access attempt`

  - Click :guilabel:`Save` to save the new Policy

.. thumbnail:: _images/policy.png

The STA configuration is complete



Azure Active Directory configuration
====================================

Open Azure Active Directory console, :menuselection:`Security --> Custom Controls` (you can use the following direct link, opens in a new tab)

|Azure|

.. |Azure| raw:: html

   <a href="https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/CustomControls" target="_blank">Azure Active Directory Console Custom - Controls</a>
