 
 # **One-OE + Hub A: One-Stack Deployment**
 
 ### Overview
 This document provides a detailed overview of the One-OE Landing Zone with Hub A addon, including its components and deployment guidance.

&nbsp; 

 ### Deployment diagram
 
<img src="one_oe_a.png" width="900" height="value">

&nbsp; 

There are two deployment options: One-Stack Deployment with **CIS Level 1** and **CIS Level 2** security controls:

- **CIS Level 1** is recommended in scenarios where:
  - CIS Level 1 Security Controls meet your security requirements.
  - You are exploring or testing configurations and need to deploy and tear down environments quickly.
  - You are creating a proof-of-concept (PoC) environment.

- **CIS Level 2** is recommended in scenarios where:
  - Your security requirements mandate CIS Level 2 Security Controls (for example, deploying a Vault to manage your encryption keys and force the encryption of all your data with them, block storage, object storage, etc.).

&nbsp; 

 ### Input Configurations for **CIS Level 1** 

| JSON configuration | Configuration-defined components | as an input to Terraform module | 
|:-|:-|:-|
| **IAM configuration**</br> [oneoe_iam.json](oci_open_lz_one-oe_iam.auto.tfvars.json) | • Compartments</br> • Identity Domain</br> • IAM groups and policies | [OCI Landing Zone IAM](https://github.com/oci-landing-zones/terraform-oci-modules-iam) |
| **Network configuration** in</br> *Step 1* - [oneoe_hub_a_network_pre.json](oci_open_lz_hub_a_network_light.auto.tfvars.json)</br> and</br> *Step 2* - [oneoe_hub_a_network.json](oneoe_hub_a_network.json) | • Hub A</br> • Two OCI Network Firewalls (DMZ and Internal) </br> • Internet, NAT and Service Gateways</br> • Dynamic Routing Gateway (DRG)</br> • Routing tables</br> • Two Spoke VCNs (Prod and  PreProd)</br> • Security Lists and NSGs</br> • One example Public Load Balancer (LBaaS) | [OCI Landing Zone Network](https://github.com/oci-landing-zones/terraform-oci-modules-networking) |
| **Security configuration** in</br> *Step 1* - [oneoe_security_cis1.json](oci_open_lz_one-oe_security_cisl1.auto.tfvars.json)</br> and</br> *Step 2* - [oneoe_security_cis1.json](oci_open_lz_one-oe_security_cisl1.auto.tfvars.json) | • Security Zones and Cloud Guard | [OCI Landing Zone Security](https://github.com/oci-landing-zones/terraform-oci-modules-security) |
| **Observability configuration** in</br> *Step 1* - [oneoe_observability_cisl1.json](oci_open_lz_one-oe_observability_cisl1.auto.tfvars.json)</br> and</br> *Step 2* - [oneoe_observability_cisl1_fllowlogs.json](oci_open_lz_one-oe_observability_cisl2_addon_flowlogs.auto.tfvars.json) | • Events</br> • Alarms</br> • Logging</br> • Notifications | [OCI Landing Zone Observability](https://github.com/oci-landing-zones/terraform-oci-modules-observability) |

&nbsp;

### Deploy with ORM

#### Step 1: 
  - Click [<img src="/commons/images/DeployToOCI.svg"  height="25" align="center">](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/oci-landing-zones/terraform-oci-modules-orchestrator/archive/refs/tags/v2.0.5.zip&zipUrlVariables={"input_config_files_urls":"https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_iam.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_hub_a_network_light.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_observability_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_security_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_governance.auto.tfvars.json"})</br>

And follow these steps:
  1. Accept terms, wait for the configuration to load.
  2. Set the working directory to “rms-facade”.
  3. Set the stack name you prefer.
  4. Set the terraform version to 1.5.x. Click Next.
  5. Accept the default files. Click Next. Optionally, replace with your json/yaml config files.
  6. Un-check run apply. Click Create.
  
#### Step 2: 
  - Below steps or some of them to be executed once Step 1 Stack and all landing zone elements are created. This step requires the update the previous ORM stack json configuration files in order to complete the Networking routing, add extra Security Zones Recipes (3, 4, and 5), and Network Flow Logs. This update can be executed in one step by replacing both files as described below.</br>
  

  1. Network routing:</br>
     - Use a configuration [oneoe_hub_a_network.json](oneoe_hub_a_network.json) and update "DMZ OCI NFW PRIVATE IP OCID" and "Internal OCI NFW PRIVATE IP OCID" with the OCID of the DMZ and Internal FW's Private IP OCID accordingly.
     - Edit the ORM stack and replace the oneoe_hub_a_network_pre.json network JSON configuration file with the oneoe_hub_a_network.json, which now contains Private IP of both OCI Network Firewalls, in the respective routing tables.
  
  2. Security Zones:</br>
    Use the configuration [oneoe_security_cis1_sz345.json](oci_open_lz_one-oe_security_cisl1_addon_sz345.auto.tfvars.json) to extend the base configuration with additional Security Zone targets to apply Recipes in the shared network compartment, the production shared network compartment, and project 1 example. As the compartment hierarchy goes deeper the Security Zones are more restrictive.</br>
    Note that this update action is not in the base stack red due to limitations with terraform dependency grapth while creating these resources. These will be merged once these limitations are solved.
  3. Observability - Flow Logs:
    Use the configuration [one_oe_observability_cisl1_flowlogs.json](oci_open_lz_one-oe_observability_cisl2_addon_flowlogs.auto.tfvars.json) to create the VCN and Subnets flow logs.</br>
    Note that by default, the VCN and Subnet flows logs are not deployed. The first 10 gigabytes of log storage are free every month. The configuration creates a log group for the shared network and each shared network environment, where it would create logs for every VCN and subnet within the VCNs. It would depend on how much traffic is generated in your VCNs/Subnets to overpass the free log storage that you get every month.



&nbsp; 

# License

Copyright (c) 2025 Oracle and/or its affiliates.

Licensed under the Universal Permissive License (UPL), Version 1.0.

See [LICENSE](/LICENSE.txt) for more details.





 