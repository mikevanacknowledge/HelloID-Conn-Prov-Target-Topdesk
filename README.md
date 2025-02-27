# HelloID-Conn-Prov-Target-Topdesk

| :information_source: Information |
|:---------------------------|
| This repository contains the connector and configuration code only. The implementer is responsible to acquire the connection details such as username, password, certificate, etc. You might even need to sign a contract or agreement with the supplier before implementing this connector. Please contact the client's application manager to coordinate the connector requirements.       |

<br />

<p align="center">
  <img src="https://user-images.githubusercontent.com/68013812/91290003-59bd2c00-e793-11ea-853f-bf974eac7005.png">
</p>

<!-- TABLE OF CONTENTS -->
## Table of Contents
* [Introduction](#introduction)
* [Connector Icon](#connector-icon)
* [Getting Started](#getting-started)
  * [Permissions](#permissions)
  * [API Access](#API-access)
* [Usage](#usage)

## Introduction
TOPdesk provides a RESTful API that allows you to programmatically interact with its services and data.

## Connector Icon
https://avatars1.githubusercontent.com/u/14311896?s=200&v=4

<!-- GETTING STARTED -->
## Getting Started

By using this connector you will have the ability to create one of the following items in TOPdesk:

* Simple changes
* Extensive changes
* Incidents
* Accounts

In this project we are connecting to the TOPdesk API using the Powershell Invoke-RestMethod cmdlet. Before we can start using this, we have to setup and configure our API access first.

### Permissions

The following permissions are required to use this connector. This should be configured on a specific Permission Group for the Operator HelloID uses.
<table>
<tr><td>Permission</td><td>Read</td><td>Write</td><td>Create</td><td>Archive</td></tr>

<tr><td><b>Call Management</b></td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td>First line calls</td><td>x</td><td>x</td><td>x</td><td>&nbsp;</td></tr>
<tr><td>Second line calls</td><td>x</td><td>x</td><td>x</td><td>&nbsp;</td></tr>
<tr><td>Escalate calls</td><td>&nbsp;</td><td>x</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td>Link object to call</td><td>&nbsp;</td><td>x</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td>Link room to call</td><td>&nbsp;</td><td>x</td><td>&nbsp;</td><td>&nbsp;</td></tr>

<tr><td><b>Change Management</b></td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td>Requests for Simple Change</td><td>x</td><td>x</td><td>x</td><td>&nbsp;</td></tr>
<tr><td>Requests for Extensive Change</td><td>x</td><td>x</td><td>x</td><td>&nbsp;</td></tr>
<tr><td>Simple Changes</td><td>x</td><td>x</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td>Extensive Changes</td><td>x</td><td>x</td><td>&nbsp;</td><td>&nbsp;</td></tr>

<tr><td><b>New Asset Management</b></td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td>Templates</td><td>x</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>

<tr><td><b>Supporting Files</b></td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td>Persons</td><td>x</td><td>x</td><td>x</td><td>x</td></tr>
<tr><td>Operators</td><td>x</td><td>x</td><td>x</td><td>x</td></tr>
<tr><td>Operator groups</td><td>x</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td>Suppliers</td><td>x</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td>Rooms</td><td>x</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td>Login data</td><td>&nbsp;</td><td>x</td><td>&nbsp;</td><td>&nbsp;</td></tr>

<tr><td><b>Reporting API</b></td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td>REST API</td><td>x</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td>Use application passwords</td><td>&nbsp;</td><td>x</td><td>&nbsp;</td><td>&nbsp;</td></tr>

</table>

(To create departments and budgetholders, you will need to allow the API account read and write access to the "Instellingen voor Ondersteunende bestanden".)

### API Access

Getting Connected to the API

 1. Go to your TOPdesk portal (e.g., https://customer.topdesk.net/), and log into an operator account.
 2. Go to Modules > Supporting Files > Overview > Permission groups.
 3. Select the New Permission Group button.
 4. Enter a Name for the permission group.
 5. Configure te correct permissions as described in the table above.
 6. Select the Save button.
 7. Select the Operators tab.
 8. Select the Links Wizard button.
 9. Select the operator whose credentials you wish to use to access the TOPdesk API.
10. Select the Link button.
11. Select the user account icon in the top-right corner of the screen, and in the drop down, select My Settings.
12. Under the Application passwords section, select the Add button.
13. Enter an Application name.
14. Select the Create button.
15. Copy the Application password.

To work with the API TOPdesk expects an application password, not the password used to login to the web interface. More information about this specific password can be found on the following [Documentation](https://developers.topdesk.com/tutorial.html#show-collapse-usage-createAppPassword) page.

For more information about the TOPdesk  API see the following TOPdesk [Documentation](https://developers.topdesk.com/tutorial.html#show-collapse-config-topdesk) page.

<!-- USAGE EXAMPLES -->
## Usage
 
When running into 403 issues when creating changes, make sure the configured change template is available for use in change requests. This option can be enabled from the second tab of the change template configuration page.

Update the scripts with your own values, under the #TOPdesk system data comment:

    url: Replace 'xxxx' with your organization's TOPdesk subdomain.
    apiKey: The application password you copied.
    userName: The TOPdesk operator username that you linked to the new permission group you created.

(Optional) 
when using the connector to handle Incidents or Changes you have to configure the path to where your exampleChanges.json or exampleIncidents.json are being stored 
    
    path = C:\Temp\Powershell\TOPDesk\exampleChanges.json

_For more information about our HelloID PowerShell connectors, please refer to our general [Documentation](https://docs.helloid.com/hc/en-us/articles/360012558020-How-to-configure-a-custom-PowerShell-target-connector) page_

It is now possible to use the manager or the employee as a requester of a change, by using the words 'employee' or the word 'manager' as a value in the 'Requester' parameter.
Please make sure the person is enabled(not archived) when setting the employee as the requester when creating a change. Usually you need to disable any action in the disable task, and archive the user in the delete task. An example for a dummy disable task is displayed below:
```powershell
#Initialize default properties
$success = $False;
$p = $person | ConvertFrom-Json
$aRef = $accountReference | ConvertFrom-Json
$auditMessage = " not disabled succesfully";

if(-Not($dryRun -eq $True)){  
    $success = $True
    $auditMessage = "disabled successfully";
}

#build up result
$result = [PSCustomObject]@{ 
	Success = $success;
	AuditDetails = $auditMessage;
};

Write-Output $result | ConvertTo-Json -Depth 10;
```

# HelloID Docs
The official HelloID documentation can be found at: https://docs.helloid.com/
