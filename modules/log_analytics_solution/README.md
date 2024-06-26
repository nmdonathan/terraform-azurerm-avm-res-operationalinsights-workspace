<!-- BEGIN_TF_DOCS -->
# Azure Log Analytics Solution

This is the sub-module to Log Analytics Solution

## Features

This module supports:

- Creates Log Analytics Solution

"Major version Zero (0.y.z) is for initial development. Anything MAY change at any time. The module SHOULD NOT be considered stable till at least it is major version one (1.0.0) or greater. Changes will always be via new versions being published and no changes will be made to existing published versions. For more details please go to <https://semver.org/>"

```hcl
resource "azurerm_log_analytics_solution" "this" {
  location              = var.log_analytics_solution_location
  resource_group_name   = var.log_analytics_solution_resource_group_name
  solution_name         = var.log_analytics_solution_solution_name
  workspace_name        = var.log_analytics_solution_workspace_name
  workspace_resource_id = var.log_analytics_solution_workspace_resource_id
  tags                  = var.log_analytics_solution_tags

  dynamic "plan" {
    for_each = [var.log_analytics_solution_plan]
    content {
      product        = plan.value.product
      publisher      = plan.value.publisher
      promotion_code = plan.value.promotion_code
    }
  }
  dynamic "timeouts" {
    for_each = var.log_analytics_solution_timeouts == null ? [] : [var.log_analytics_solution_timeouts]
    content {
      create = timeouts.value.create
      delete = timeouts.value.delete
      read   = timeouts.value.read
      update = timeouts.value.update
    }
  }
}
```

<!-- markdownlint-disable MD033 -->
## Requirements

The following requirements are needed by this module:

- <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) (~> 1.5)

- <a name="requirement_azurerm"></a> [azurerm](#requirement\_azurerm) (~> 3.71)

## Providers

The following providers are used by this module:

- <a name="provider_azurerm"></a> [azurerm](#provider\_azurerm) (~> 3.71)

## Resources

The following resources are used by this module:

- [azurerm_log_analytics_solution.this](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/log_analytics_solution) (resource)

<!-- markdownlint-disable MD013 -->
## Required Inputs

The following input variables are required:

### <a name="input_log_analytics_solution_location"></a> [log\_analytics\_solution\_location](#input\_log\_analytics\_solution\_location)

Description: (Required) Specifies the supported Azure location where the resource exists. Changing this forces a new resource to be created.

Type: `string`

### <a name="input_log_analytics_solution_plan"></a> [log\_analytics\_solution\_plan](#input\_log\_analytics\_solution\_plan)

Description: - `product` - (Required) The product name of the solution. For example `OMSGallery/Containers`. Changing this forces a new resource to be created.
- `promotion_code` - (Optional) A promotion code to be used with the solution. Changing this forces a new resource to be created.
- `publisher` - (Required) The publisher of the solution. For example `Microsoft`. Changing this forces a new resource to be created.

Type:

```hcl
object({
    product        = string
    promotion_code = optional(string)
    publisher      = string
  })
```

### <a name="input_log_analytics_solution_resource_group_name"></a> [log\_analytics\_solution\_resource\_group\_name](#input\_log\_analytics\_solution\_resource\_group\_name)

Description: (Required) The name of the resource group in which the Log Analytics solution is created. Changing this forces a new resource to be created. Note: The solution and its related workspace can only exist in the same resource group.

Type: `string`

### <a name="input_log_analytics_solution_solution_name"></a> [log\_analytics\_solution\_solution\_name](#input\_log\_analytics\_solution\_solution\_name)

Description: (Required) Specifies the name of the solution to be deployed. See [here for options](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions).Changing this forces a new resource to be created.

Type: `string`

### <a name="input_log_analytics_solution_workspace_name"></a> [log\_analytics\_solution\_workspace\_name](#input\_log\_analytics\_solution\_workspace\_name)

Description: (Required) The full name of the Log Analytics workspace with which the solution will be linked. Changing this forces a new resource to be created.

Type: `string`

### <a name="input_log_analytics_solution_workspace_resource_id"></a> [log\_analytics\_solution\_workspace\_resource\_id](#input\_log\_analytics\_solution\_workspace\_resource\_id)

Description: (Required) The full resource ID of the Log Analytics workspace with which the solution will be linked. Changing this forces a new resource to be created.

Type: `string`

## Optional Inputs

The following input variables are optional (have default values):

### <a name="input_log_analytics_solution_tags"></a> [log\_analytics\_solution\_tags](#input\_log\_analytics\_solution\_tags)

Description: (Optional) A mapping of tags to assign to the resource.

Type: `map(string)`

Default: `null`

### <a name="input_log_analytics_solution_timeouts"></a> [log\_analytics\_solution\_timeouts](#input\_log\_analytics\_solution\_timeouts)

Description: - `create` - (Defaults to 30 minutes) Used when creating the Log Analytics Solution.
- `delete` - (Defaults to 30 minutes) Used when deleting the Log Analytics Solution.
- `read` - (Defaults to 5 minutes) Used when retrieving the Log Analytics Solution.
- `update` - (Defaults to 30 minutes) Used when updating the Log Analytics Solution.

Type:

```hcl
object({
    create = optional(string)
    delete = optional(string)
    read   = optional(string)
    update = optional(string)
  })
```

Default: `null`

## Outputs

The following outputs are exported:

### <a name="output_resource"></a> [resource](#output\_resource)

Description: this is the resource of the rule collection group

### <a name="output_resource_id"></a> [resource\_id](#output\_resource\_id)

Description: the resource id of the rule\_collection\_group

## Modules

No modules.

<!-- markdownlint-disable-next-line MD041 -->
## Data Collection

The software may collect information about you and your use of the software and send it to Microsoft. Microsoft may use this information to provide services and improve our products and services. You may turn off the telemetry as described in the repository. There are also some features in the software that may enable you and Microsoft to collect data from users of your applications. If you use these features, you must comply with applicable law, including providing appropriate notices to users of your applications together with a copy of Microsoft’s privacy statement. Our privacy statement is located at <https://go.microsoft.com/fwlink/?LinkID=824704>. You can learn more about data collection and use in the help documentation and our privacy statement. Your use of the software operates as your consent to these practices.
<!-- END_TF_DOCS -->