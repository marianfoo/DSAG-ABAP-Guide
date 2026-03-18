---
layout: page
title: Screen Personas 
permalink: /security/screen-personas/
parent: Security
nav_order: 8
---

{: .no_toc}

# SAP Screen Personas 3.0

1. TOC
{:toc}

## Allgemein

What are “SAP Screen Personas 3.0”?

From the [SAP Onlinehilfe](https://help.sap.com/docs/SAP_SCREEN_PERSONAS/e9aec5d380204249836a4fc3fc76f38e/d59f3aac0f574537af49f2ce0033bba8.html):

_SAP Screen Personas 3.0 supports the transformation of classic applications into user-centric UIs tailored to specific application roles and business needs. The simplified versions of classic applications are called flavors. These custom UIs can be used for one or more images within a classic application or across applications. The flavors are independent of the underlying transactions and can be targeted to specific application roles. A classic application can have multiple flavors. For example, there can be a specific flavor per user group._

Technically, SAP Screen Personas 3.0 (Personas) is based on a SICF service that starts a preconfigured service of the SAP GUI for HTML under the standard node /sap/bc/personas. The engine has its own services under the standard node host/sap/bc/se. This means that the security measures for the SAP GUI for HTML and ITS generally also apply to Screen Personas and its services.

![SICF Service](./img/image21.png)

SICF Service
{: .img-caption}

SAP Screen Personas is a user interface technology that is implemented as an add-on in the backend system. Security is therefore dependent on the functions available for this system. Most of these system functions are dictated by the underlying system mechanisms and policies. Any aspects specific to SAP Screen Personas or potential discrepancies and areas of particular interest are discussed below.

## Spezielle Sicherheitsaspekte

### SSL encryption of the connection

The services used by Personas must be encrypted using SSL:

![Encryption](./img/image22.png)

Encryption
{: .img-caption}

### Cross site request forgery protection for ITS

To protect cross site requests, the parameter ~XSRFCHECK = 1 must be set in the services under GUI configuration. Details are described in note 1481392.

![Parametereinstellung](./img/image23.png)

Parametereinstellung
{: .img-caption}

## General recommendations for ITS and SAP GUI for HTML

### Enable logout for SAP GUI for HTML

To ensure that logging out of the HTML GUI works safely, the following things must be taken into account:

- Logoff service must be activated in ICF → Activate service tree /sap/public/bc/icf/logoff
- The logoff service must be stored as a logout page in the HTML GUI service and in the personas services

![Abmeldung Web-GUI](./img/image24.png)

Abmeldung Web-GUI
{: .img-caption}

On the logoff page of the WEBGUI service, specify the service /sap/public/bc/icf/logoff as a redirect.

{: .note }
> Details are described in SAP note 1777513 (as well as further background information)

### Domain Relaxing deaktivieren (falls notwendig)

Domain relaxing allows client-side (e.g. on a browser) functions or applications to communicate with other client-side functions in other client windows. Domain relaxing is necessary if applications from different backend systems (servers) need to exchange data at the frontend. It must be ensured that the same client domain is set for all affected applications, otherwise the client (browser) will complain about an access error when attempting to communicate.

If such browser behavior occurs, domain relaxing must be deactivated. To do this, the ~no_domain_relaxing parameter is added to the service's GUI configuration and set to 1 (one).

![Domain Relaxing](./img/image25.png)

Domain Relaxing
{: .img-caption}

{: .note }
> Details are described in SAP Note 2111099 (as well as further background information)

## SAP Berechtigungen

SAP Screen Personas 3.0 is enabled for a user only if they have the required permissions based on user role. Role assignment occurs as part of the regular user management process. SAP delivers the following standard roles:

- Administrator: **/PERSONAS/ADMIN_ROLE** \- This role has full access to all functions available to the flavor consumer at runtime, can provide access to all functions of the flavor builder tasks at design time, and can perform administration tasks in the administration environment.
- Flavor Consumer: **/PERSONAS/CONSUMER_ROLE** \- This role has permissions to access flavors for classic applications. Flavor consumers can use the Flavor Manager to choose between flavors and the original image and move flavors between the Flavor Manager and the Flavor Gallery.
- Flavor Builder: **/PERSONAS/EDITOR_ROLE** \- This role is used to create flavors and other user-owned objects with editing rights in all Design Time editors.

SAP delivers the roles without a generated authorization profile, so the profile must be generated and most likely also adjusted.

Basically: Users must always have access to the transaction code, in addition to what belongs to them in SAP Screen Personas, in order to be able to perform a function within Personas. So TCD (application authorization) plus Personas authorizations must be present.

The following tables explain how Personas uses the various permission objects to create flavors and distributes them using the roles shipped by default:

![Screen Personas Berechtigungen (Teil 1)](./img/image26.png)

Screen Personas Berechtigungen (Teil 1)
{: .img-caption}

![Screen Personas Berechtigungen (Teil 2)](./img/image27.png)

Screen Personas Berechtigungen (Teil 2)
{: .img-caption}

![Screen Personas Berechtigungen (Teil 3)](./img/image28.png)

Screen Personas Berechtigungen (Teil 3)
{: .img-caption}