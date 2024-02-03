# Azure Resource Manager (ARM)

This repository aims to create highly flexible but (hopefully) simple to use ARM templates. The repository is broken down into two sections: [Resources](https://github.com/MattDaines/Azure-ARM/tree/main/Resource) and [Patterns](https://github.com/MattDaines/Azure-ARM/tree/main/Patterns). Templates within the Resources section, generally, contain a single resource that can either be deployed on their own or utilised by a pattern template. Pattern templates will mostly contain linked resources referencing templates within the *Resources* folder.

## Contributing

I can't lie that I'm a little new to open-source on Github, so there's likely going to be some learning required on my part along the way. I think and hope that I've setup some branch security so that branches are required to either start with *resource/*, *pattern/* or *docs/* - if that even matters for open-source. Some additional "rules" that I think should be followed:

- All templates files should be named azuredeploy.json
- All parameter files should be named azuredeploy.parameters.json
- All Resource and Patterns should contain at least an azuredeploy.json template
- All Patterns should reference Resource templates within this repository (so patterns are less likely to randomly break)
- All templates should contain a README.md for documenting how the template can be deployed
- Docs/* branches should only update README.md files
- Resources/* branches should only update templates within the Resources directory and the resources README
- Patterns/* branches should only update templates within the Patterns directory, any dependant resources and both pattern and resource READMEs
- Patterns can utilise other patterns within this repository
- In the event that PowerShell scripts are committed, scripts should not use AzureRM cmdlets. Instead scripts should use the Az cmdlets

## Helpful Resources

| Resource | Description |
| - | - |
| [ARM Template Documentation](https://docs.microsoft.com/en-gb/azure/azure-resource-manager/templates/) | Where you can find (nearly) all information on how to build ARM templates |
| [ARM Template Reference](https://docs.microsoft.com/en-us/azure/templates/) | Where you can find (nearly) all information about Azure resource types and their properties |
| [ARM Template Schema](https://github.com/Azure/azure-resource-manager-schemas) | Used when the ARM template reference might not document in enough detail |
| [Resource Explorer](https://resources.azure.com/) | Similar to export template from the Azure Portal, this tool allows you to see most deployed Azure resources in a JSON format |
| [Azure Quick Start Templates](https://github.com/Azure/azure-quickstart-templates) | A good resource for troubleshooting templates or building your first templates |
