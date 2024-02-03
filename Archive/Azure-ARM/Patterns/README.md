# Patterns

This directory should contain templates that are capable of deploying more complex patterns of Azure resource by using templates within the [Resources](https://github.com/MattDaines/Azure-ARM/tree/main/Resource) directory.

The directory structure is likely to be a bit more difficult here. So initially, while I build out the repository, I'm going to keep it relatively flat. Each Pattern should be contained within a single directory with a descriptive name. Each Pattern should contain at least a template (named azuredeploy.json) and a README.

Resource Templates should contain a README that may or may not contain a *Required By* section. If you're developing a new pattern, you should add a link to this pattern in the Required By section of a Resource's README file. If the section doesn't yet exist, it should be added. The Pattern should also contain a *Required By* section as Patterns can depend on other Patterns. I expect that Pattern "Required By" details will be more up to date than Resource's README as time goes on and therefore Pattern documentation will override resource pattern *Required By* details.
