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
|[Batch Update Active Alert Tags](../event/batch_update_active_alert_tags.html)| Batch update the tags for the specified alerts |
|[Create Alert Rule](../event/create_alert_rule.html)   |  Create a new alert rule|
|[Update Alert Rule](../event/update_alert_rule.html)        |   Update an alert rule     |
|[Delete Alert Rule](../event/delete_alert_rule.html)    |  Delete all the rules under the organization as per the alert rule IDs      |
|   [Create Alert Content](../event/create_alert_content.html)     |   Create a new alert content   |
|  [Update Alert Content](../event/update_alert_content.html)      |    Update an alert content         |
|     [Delete Alert Content](../event/delete_alert_content.html)   |    Delete an alert content        |
|    [Create Alert Severity](../event/create_alert_severity.html)    | Create a new alert severity  |
|  [Update Alert Severity](../event/update_alert_severity.html)      |  Update an alert severity       |
|     [Delete Alert Severity](../event/delete_alert_severity.html)   |   Delete an alert severity     |
|  [Create Alert Type](create_alert_type.html)      | Create a new alert type |
|  [Update Alert Type](../event/update_alert_type.html)      |   Update an alert type      |
|  [Delete Alert Type](../event/delete_alert_type.html)      |  Delete an alert type |
|  [Create Active Alert](../event/create_active_alert.html)      | Create a new active alert |
|   [Delete Active Alert](../event/delete_active_alert.html)     |Delete a specified active alert      |
|   [Create History Alert](../event/create_history_alert.html) |  Create a new history alert  |


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