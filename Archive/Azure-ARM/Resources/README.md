# Resources

This directory should contain templates that are capable of deploying a single resource. Exceptions are of course okay and expected. However complex templates should be broken down into their smaller templates where a [pattern](https://github.com/MattDaines/Azure-ARM/tree/main/Patterns) can reuse the resources.

Directories should follow a similar but preferably identical path to the resource type followed by the template version. For example, a Storage Account could be placed under the directory `Microsoft.Storage/storageAccounts/1.0.0.0/`. This means it's significantly less likely that patterns will break if a resource type is updated.

Finally, though more relevant to pattern development, we should do our best in ensuring there is a *Required By* section in the README's for resources and that it is updated when a pattern depends on a resource. If a resource is updated and there is nothing depending on the older version we can look to remove the older versions. Resources should not depend on other Resources - if it's required, it's likely the template is becoming a pattern. That said, it doesn't mean you cannot use `dependsOn: []` within an ARM template.
