 
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

---

 ### Input Configurations for **CIS Level 1** 

| JSON configuration | Configuration-defined components | Terraform module that processes configuration | 
|:-|:-|:-|
| **IAM configuration**</br> [oneoe_iam.json](oci_open_lz_one-oe_iam.auto.tfvars.json) | • Compartments</br> • Identity Domain</br> • IAM groups and policies | [OCI Landing Zone IAM](https://github.com/oci-landing-zones/terraform-oci-modules-iam) |
| **Network configuration** for</br> *Step 1*: [oneoe_hub_a_network_pre.json](oci_open_lz_hub_a_network_light.auto.tfvars.json)</br> and</br> *Step 2*: [oneoe_hub_a_network.json](oneoe_hub_a_network.json) | • Hub A</br> • OCI Network Firewalls (DMZ & Internal) </br> • Internet, NAT, and Service Gateways</br> • Dynamic Routing Gateway (DRG)</br> • Routing Tables</br> • Two Spoke VCNs (Prod & PreProd)</br> • Security Lists (SLs) & Network Security Groups (NSGs)</br> • Public Load Balancer ([free tier LBaaS](https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm#loadbalancing), for example purposes) | [OCI Landing Zone Network](https://github.com/oci-landing-zones/terraform-oci-modules-networking) |
| **Security configuration** for</br> *Step 1*: [oneoe_security_cis1.json](oci_open_lz_one-oe_security_cisl1.auto.tfvars.json)</br> and</br> *Step 2*: [oneoe_security_cis1_sz345.json](oci_open_lz_one-oe_security_cisl1.auto.tfvars.json) | • Security Zones and Cloud Guard | [OCI Landing Zone Security](https://github.com/oci-landing-zones/terraform-oci-modules-security) |
| **Observability configuration** for</br> *Step 1*: [oneoe_observability_cisl1.json](oci_open_lz_one-oe_observability_cisl1.auto.tfvars.json)</br> and</br> *Step 2*: [oneoe_observability_cisl1_fllowlogs.json](oci_open_lz_one-oe_observability_cisl1_addon_flowlogs.auto.tfvars.json) | • Events</br> • Alarms</br> • Logging</br> • Notifications | [OCI Landing Zone Observability](https://github.com/oci-landing-zones/terraform-oci-modules-observability) |



| JSON configuration | Configuration-defined components | 
|:-|:-|
| **IAM configuration**</br> [oneoe_iam.json](oci_open_lz_one-oe_iam.auto.tfvars.json) | • Compartments</br> • Identity Domain</br> • IAM groups and policies |
| **Network configuration** for</br> *Step 1*: [oneoe_hub_a_network_pre.json](oci_open_lz_hub_a_network_light.auto.tfvars.json)</br> and</br> *Step 2*: [oneoe_hub_a_network.json](oneoe_hub_a_network.json) | • Hub A</br> • OCI Network Firewalls (DMZ & Internal) </br> • Internet, NAT, and Service Gateways</br> • Dynamic Routing Gateway (DRG)</br> • Routing Tables</br> • Two Spoke VCNs (Prod & PreProd)</br> • Security Lists (SLs) & Network Security Groups (NSGs)</br> • Public Load Balancer ([free tier LBaaS](https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm#loadbalancing), for example purposes) |
| **Security configuration** for</br> *Step 1*: [oneoe_security_cis1.json](oci_open_lz_one-oe_security_cisl1.auto.tfvars.json)</br> and</br> *Step 2*: [oneoe_security_cis1_sz345.json](oci_open_lz_one-oe_security_cisl1.auto.tfvars.json) | • Security Zones and Cloud Guard |
| **Observability configuration** for</br> *Step 1*: [oneoe_observability_cisl1.json](oci_open_lz_one-oe_observability_cisl1.auto.tfvars.json)</br> and</br> *Step 2*: [oneoe_observability_cisl1_fllowlogs.json](oci_open_lz_one-oe_observability_cisl1_addon_flowlogs.auto.tfvars.json) | • Events</br> • Alarms</br> • Logging</br> • Notifications |

&nbsp;

### Deploy with OCI Resource Manager (ORM) - CIS Level 1

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
  - The following steps, or only those relevant to your deployment - should be performed after the **Step 1** stack and all Landing Zone components have been deployed. This phase involves updating the **Step 1** ORM stack to complete Network routing, add additional Security Zone Recipes, and enable Network Flow Logs. All required updates can be applied in a single operation by replacing the corresponding configuration files as described below.
  

  1. **Network routing**:</br>
     - Use the [oneoe_hub_a_network_pre.json](oneoe_hub_a_network_pre.json) configuration file and update the fields "DMZ OCI NFW PRIVATE IP OCID" and "Internal OCI NFW PRIVATE IP OCID" with the corresponding Private IP OCIDs of the DMZ and Internal OCI Network Firewalls deployed in Step 1.
     - After updating the file, edit the ORM stack and replace the previous oneoe_hub_a_network_pre.json network configuration with oneoe_hub_a_network.json. This updated JSON file now includes the Private IPs (OCIDs) for both OCI Network Firewalls and ensures they are referenced correctly in the associated routing tables.
  
  2. **Security Zones**:</br>
    Use the configuration [oneoe_security_cis1_sz345.json](oci_open_lz_one-oe_security_cisl1_addon_sz345.auto.tfvars.json) to extend the base configuration with additional Security Zone targets to apply Recipes in the shared network compartment, the production shared network compartment, and project 1 example. As the compartment hierarchy goes deeper the Security Zones are more restrictive.</br>
    !!! Note that this update action is not in the base stack red due to limitations with terraform dependency grapth while creating these resources. These will be merged once these limitations are solved.
  3. **Observability - Flow Logs**:</br>
    Use the configuration [oneoe_observability_cisl1_flowlogs.json](oci_open_lz_one-oe_observability_cisl2_addon_flowlogs.auto.tfvars.json) to create the VCN and Subnets flow logs.</br>
    Note that by default, the VCN and Subnet flows logs are not deployed. The first 10 gigabytes of log storage are free every month. The configuration creates a log group for the shared network and each shared network environment, where it would create logs for every VCN and subnet within the VCNs. It would depend on how much traffic is generated in your VCNs/Subnets to overpass the free log storage that you get every month.

&nbsp; 

Once all required updates are applied, redeploy the ORM stack.

&nbsp;

---

&nbsp; 

 ### Input Configurations for **CIS Level 2** 

| JSON configuration | Configuration-defined components | Terraform module that processes configuration | 
|:-|:-|:-|
| **IAM configuration**</br> [oneoe_iam.json](oci_open_lz_one-oe_iam.auto.tfvars.json) | • Compartments</br> • Identity Domain</br> • IAM groups and policies | [OCI Landing Zone IAM](https://github.com/oci-landing-zones/terraform-oci-modules-iam) |
| **Network configuration** for</br> *Step 1*: [oneoe_hub_a_network_pre.json](oci_open_lz_hub_a_network_light.auto.tfvars.json)</br> and</br> *Step 2*: [oneoe_hub_a_network.json](oneoe_hub_a_network.json) | • Hub A</br> • OCI Network Firewalls (DMZ & Internal) </br> • Internet, NAT, and Service Gateways</br> • Dynamic Routing Gateway (DRG)</br> • Routing Tables</br> • Two Spoke VCNs (Prod & PreProd)</br> • Security Lists (SLs) & Network Security Groups (NSGs)</br> • Public Load Balancer ([free tier LBaaS](https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm#loadbalancing), for example purposes) | [OCI Landing Zone Network](https://github.com/oci-landing-zones/terraform-oci-modules-networking) |
| **Security configuration** for</br> *Step 1*: [oneoe_security_cis2.json](oci_open_lz_one-oe_security_cisl1.auto.tfvars.json)</br> and</br> *Step 2*: [oneoe_security_cis2_sz345.json](oci_open_lz_one-oe_security_cisl2.auto.tfvars.json) | • Security Zones and Cloud Guard | [OCI Landing Zone Security](https://github.com/oci-landing-zones/terraform-oci-modules-security) |
| **Observability configuration** for</br> *Step 1*: [oneoe_observability_cisl2.json](oci_open_lz_one-oe_observability_cisl2.auto.tfvars.json)</br> and</br> *Step 2*: [oneoe_observability_cisl2_fllowlogs.json](oci_open_lz_one-oe_observability_cisl2_addon_flowlogs.auto.tfvars.json) | • Events</br> • Alarms</br> • Logging</br> • Notifications | [OCI Landing Zone Observability](https://github.com/oci-landing-zones/terraform-oci-modules-observability) |

&nbsp;

### Deploy with OCI Resource Manager (ORM) - CIS Level 2

#### Step 1: 
  - Click [<img src="/commons/images/DeployToOCI.svg"  height="25" align="center">](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/oci-landing-zones/terraform-oci-modules-orchestrator/archive/refs/tags/v2.0.5.zip&zipUrlVariables={"input_config_files_urls":"https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_iam.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_hub_a_network_light.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_observability_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_security_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_governance.auto.tfvars.json"})</br>
  
And follow the the same steps as described for **CIS Level 1** deployment.

---

&nbsp;

# License

Copyright (c) 2025 Oracle and/or its affiliates.

Licensed under the Universal Permissive License (UPL), Version 1.0.

See [LICENSE](/LICENSE.txt) for more details.





 