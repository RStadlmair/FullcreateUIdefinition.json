# FullcreateUIdefinition.json

Sample createuidefinition.json file for Azure Marketplace and Managed Applications with all possible options for reference and your experiments.
If you are working on a Marketplace App or managed Application, this may help yu to understand the options of the creatrUIdefinitions file.
The sample provided can be sideloaded in your azure subscription and tested there, so you see how things in the file apprear in the web browser.

** This is work in progress and gets (hopefully) updated on a regular basis.

## Prerequisited

### Azure Subscription authentication

You need to be authenticated to an Azure subsriptions with an account that has contributor rights

### Az.* Modules

The sideload script was originally written for the (old) AzureRM Modules. i have modified it to run with the new az.* modules
be sure you have the following modules installed.

* Az.Accounts -RequiredVersion 1.3.0
* Az.Compute -RequiredVersion 1.3.0
* Az.Network -RequiredVersion 1.2.0
* Az.Storage -RequiredVersion 1.1.1
* Az.Resources -RequiredVersion 1.1.2


## Notes and Links

[Main documentation from the Microsoft docs website:](https://docs.microsoft.com/en-us/azure/managed-applications/publish-service-catalog-app)

[Managed App Samples on Github:](https://github.com/Azure/azure-managedapp-samples)

[Github Repository with original schema files:](https://github.com/Azure/azure-resource-manager-schemas/tree/master/schemas/0.1.2-preview)

## Editing

I use VS Code to edit the files with the following extensions:

* Azure Account
* Azure ARM Template Helper
* Azure Resource Manager Snippets
* Azure Resource Manager Templates

Important rules to consider when creating UI definitions.
Each createUIdefinitions.json file consists of the header and three elements "basic", "steps" and "outputs"

Typically when you edit a UI definition, VS Code offes you which options you can use through the schema (i guess).

## General hints on createUIdefintion.JSON files:

### Basic

In the basics section, you can in general only use the Microsoft.Common.* elements and elements which do not require the users subscription, resource group or location. 

### Steps

Enter your questions here to collect all parameters for your ARM Template.
Make sure you always have the following elements in your steps configuration, otherwise the ui will not load.

* name (unique name for referencing the element in output and in functions)
* label: (shows up in the menu)
* bladeSubtitle with pre and post validation messages for sart and end of the questionaire
* bladeTitle
* bladeSubtitle

### Output

This must match the parameters section of the target ARM Template 1:1 if this is not the case, your deployment will not work.

If you specify a parameter in steps which emits data (i.e. a Textbox), but dont reference it in the output section, the value will still be emitted with its label as name. This can lead to confisuin between the CreateUIdefinition.JSON output and the ARM-template.

If you have any typos in the outputs section, the template will not raise an error, but you may not get the results you want, so take care here and test, test, test.

### Extended testing of outputs

As Outputs cannot be tested with sideloading, i am currently working on an ARM-Template which created a resource group and sets resource tags with outputparameter = value.
Ths is in development

## Notes on UI Elements

### Microsoft.Compute.SizeSelector

The "size" parameter defines how many VM´s will be created at once. Example: You select size "Standard_D1" and size=2, the selection windows shows 2x"Standard_D1", but the output is still "Standard_D1".

## Test the UI before you do your deployment !

Test the UI always until the end. a section may work, but its important to know if also your output values are correct.

A problem i ran into when trying to all at once is that i edited the ARM template and the UI definition file in paralles - BAD IDEA
First - test the UI, and only if this works combine it with the ARM template - saves a lot of time.
Testing the UI is described here [Testing UI files:](https://docs.microsoft.com/en-us/azure/managed-applications/test-createuidefinition) and a modified version of the PowerShell script using the Az.* modules is linked in this repo.

So, create your UI using the followinf steps

* [ ] Create an ARM Template which works with parameters coming from a parameter template file or a parameter object
* [ ] Be sure the template works and collect the parameters needed
* [ ] Create the UI and test it in the portal
* [ ] Combine UI and ARM Template

Happy testing / developing

Roman
