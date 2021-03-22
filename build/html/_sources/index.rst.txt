.. SafeNet Trusted Access documentation master file, created by
   sphinx-quickstart on Mon Mar 22 11:01:57 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Azure Custom Authentication Factors with SafeNet Trusted Access
===============================================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:


Overview
========

Azure Custom Authentication Factors (Custom Controls) allows extending the Azure Active Directory authentication with a third party authentication provider, using OIDC protocol.
When using custom controls, the users are redirected to SafeNet Trusted Access to satisfy authentication requirements outside of Azure Active Directory. To satisfy this control, a user's browser is redirected to SafeNet Trusted Access, performs any required authentication, and is then redirected back to Azure Active Directory. Azure Active Directory verifies the response and, if the user was successfully authenticated or validated, the user continues in the Conditional Access flow.


.. blockdiag::

    blockdiag azure {
      
      node_width=350;  
      node_height=200;
      default_fontsize = 35;
      
      
      A [label = "Azure\n Active Directory"];
      B [label = "AAD Username"];
      C [label = "AAD Password"];
      D [label = "STA Authentication"];
      
      A -> B -> C -> D -> A;
      
    }




