# FullcreateUIdefinition.json
Sample createuidefinition.json file for Azure Marketplace and Managed Applications with all possible options for reference and your experiments.

##Notes and Links:
Main documentation from the Microsoft docs website:
https://docs.microsoft.com/en-us/azure/managed-applications/publish-service-catalog-app

Managed App Samples on Github:
https://github.com/Azure/azure-managedapp-samples

##Editing:
I use VS Code to edit the files with the following extensions:
* Azure Account
* Azure ARM Template Helper
* Azure Resource Manager Snippets
* Azure Resource Manager Templates

Important rules to consider when creating UI definitions.
Each createUIdefinitions.json file consists of the header and three elements "basic", "steps" and "outputs"

Typically when you edit a UI definition, VC Code offes you which options you can use through the schema (i guess).

##General hints on createUIdefintion.JSON files:

###Basic: 
In the basics section, you can in general only use the Microsoft.Common.* elements and elements which do not require the users subscription, resource group or location. 

###Steps:
Enter your questions here to collect all parameters for your ARM Template

###Output:
This must match the parameters section of the target ARM Template 1:1 if this is not the case, your deployment will not work

##Test the UI before you do y deployment !!
A problem i ran into when trying to all at once is that i edited the ARM template and the UI definition file in paralles - BAD IDEA
First - test the UI, and only if this works combine it with the ARM template - saves a lot of time.
Testing the UI is described here https://docs.microsoft.com/en-us/azure/managed-applications/test-createuidefinition and a modified version of the PowerShell script using the Az.* modules is linked in this repo.

