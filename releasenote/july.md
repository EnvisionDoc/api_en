# 2019/08/08


## Connection Service

### New APIs

| API                          | Description    |
|:---------------------------------|:---------|
| [Replace Device](../connect/replace_device.html) | Replace the Device Key of a device without changing its asset ID (`assetId`) |

### Changed APIs


<table>
            <tr align="left">
                <th>API</th>
				<th>Description</th>
            </tr>
            <tr>
                <td><a href="../connect/create_product.html">Create Product</a></td>
				<td>2 new optional parameters: <code>dynamicActivateEnabled</code> and <code>productTags</code> are supported in request body.
				<ul>
				<li><code>dynamicActivateEnabled</code>: indicate whether to activate the product dynamically</li>
            	<li><code>productTags</code>: indicate the product tags</li>
				</ul>
            </td>
            </tr>
            <tr>
                <td><a href="../connect/update_product.html">Update Product</a></td>
				<td>A new optional parameter <code>productTags</code> is supported in request body, which indicates the product tags</td>
            </tr>
            
</table>



### Resolved Issues


| API                        | Description        |
|:-------------------------------|:-------------------------|
| [Create Device](../connect/create_device.html) | The parameter `deviceTags` in the request body was invalid |


## Alert Service

### New APIs

| API     | Description           |
|:--------------|:---------------------|
|[Batch Update Active Alert Tags](../event/batch_update_active_alert_tags.html)| Batch update the tag for the specified alerts |
|[Create Alert Rule](../event/create_alert_rule.html)   |  A new alert rule will be created.             |
|[Update Alert Rule](../event/update_alert_rule.html)        |   An alert rule will be updated      |
|[Delete Alert Rule](../event/delete_alert_rule.html)    |  Delete all the rules under the organization as per the alert rule IDs      |
|   [Create Alert Content](../event/create_alert_content.html)     |   An alert content will be deleted      |
|  [Update Alert Content](../event/update_alert_content.html)      |    An alert content will be updated          |
|     [Delete Alert Content](../event/delete_alert_content.html)   |    An alert content will be deleted         |
|    [Create Alert Severity](../event/create_alert_severity.html)    | An alert severity will be created          |
|  [Update Alert Severity](../event/update_alert_severity.html)      |  An alert severity will be updated        |
|     [Delete Alert Severity](../event/delete_alert_severity.html)   |   An alert severity will be deleted     |
|  [Create Alert Type](create_alert_type.html)      | An alert type will be created     |
|  [Update Alert Type](../event/update_alert_type.html)      |   An alert type will be updated           |
|  [Delete Alert Type](../event/delete_alert_type.html)      |  An alert type will be deleted            |
|  [Create Active Alert](../event/create_active_alert.html)      | An active alert will be created       |
|   [Delete Active Alert](../event/delete_active_alert.html)     |A specified alert will be deleted           |
|   [Create History Alert](../event/create_history_alert.html) |  A history alert will be created |


### Changed APIs


<table>
            <tr align="left">
                <th>API</th>
				<th>Description</th>
            </tr>
            <tr>
                <td><a href="../event/search_active_alerts.html">Search Active Alerts</a></td>
				<td>2 optional parameters: <code>scope</code> and <code>rootAlert</code> are supported in request body.
				<ul>
				<li><code>scope</code>: Query the alerts in a specified asset tree or in an asset node on the asset tree, and specify whether to return the blocked derivative alerts. This parameter cannot be applied with <code>rootAlert</code>. Data type is "Scope Structure".</li>
            	<li><code>rootAlert</code>: Query the derivative alerts which are blocked by the specified root alert. This parameter cannot be applied with <code>scope</code>. Data type is "RootAlert Structure".</li>
				</ul>
            </td>
            </tr>
            <tr>
                <td><a href="../event/search_history_alerts.html">Search History Alerts</a></td>
				<td>2 optional parameters: <code>scope</code> and <code>rootAlert</code> are supported in request body.
				<ul>
				<li><code>scope</code>: Query the alerts in a specified asset tree or in an asset node on the asset tree, and specify whether to return the blocked derivative alerts. This parameter cannot be applied with <code>rootAlert</code>. Data type is "Scope Structure".</li>
            	<li><code>rootAlert</code>: Query the derivative alerts which are blocked by the specified root alert. This parameter cannot be applied with <code>scope</code>. Data type is "RootAlert Structure".</li>
				</ul>
            </td>
            </tr>
            
</table>