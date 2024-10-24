# 1.0.5 (10/23/2024)
---
This release adds an additional field to the monitoring configuration to distinguish different monitored SD-WAN Managers from one another.
The new "Manager Name" field in the monitoring configuration will attach to metrics as the dimension `manager_name`.

This version of the extension is not backwards-compatible due to the new field. Please back up your existing monitoring configurations
prior to replacing them with new ones.


# 1.0.3 (10/22/2024)
---
This release updates the extension to be built properly for both Linux and Windows compatibility.


# 1.0.2 (7/17/2024)
---
Update package declarations following new Dynatrace developer documentation.


# 1.0.0 (6/21/2024)
---
Initial release of the extension.
