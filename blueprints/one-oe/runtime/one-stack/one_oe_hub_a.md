 
 # **One-OE + Hub A: One-Stack Deployment**
 
 ### Overview
 This document provides a detailed overview of the One-OE Landing Zone with Hub A addon, including its components and deployment guidance.

 ### Deployment Diagram
 

 ### Input Configurations

| JSON configuration | Configuration-defined components | Terraform module | 
|:-|:-|:-|
| [**IAM Configuration**](oci_open_lz_one-oe_iam.auto.tfvars.json) | Compartments, Identity Domain, IAM groups, policies | [OCI Landing Zone IAM](https://github.com/oci-landing-zones/terraform-oci-modules-iam) |
| [**Network Configuration**](oci_open_lz_hub_a_network_light.auto.tfvars.json) | Hub A, two OCI Network Firewalls (DMZ, Internal), Internet GW, NAT GW, Service GW, DRG, Routing tables, two Spoke VCNs (Prod, PreProd), Security Lists, NSGs| [OCI Landing Zone Network](https://github.com/oci-landing-zones/terraform-oci-modules-networking) |
| [**Security Configuration**](oci_open_lz_one-oe_security_cisl1.auto.tfvars.json) | Security Zones, Cloud Guard | [OCI Landing Zone Security](https://github.com/oci-landing-zones/terraform-oci-modules-security) |
| [**Observability Configuration**](oci_open_lz_one-oe_observability_cisl1.auto.tfvars.json) | Events, Alarms, Logging, and Notifications | [OCI Landing Zone Observability](https://github.com/oci-landing-zones/terraform-oci-modules-observability) |



 
### Deplyment
|| One-Stack Deployment with CIS Level 1 Security Controls | One-Stack Deployment with CIS Level 2 Security Controls | 
|:-|:-|:-|
| USE | This option is recommended in scenarios where:</br> • CIS Level 1 Security Controls meet your security requirements.</br> • You are exploring or testing configurations and need to deploy and tear down environments quickly.</br> • You are creating a proof-of-concept (PoC) environment. | This option is recommended in scenarios where:</br> • Your security requirements mandate CIS Level 2 Security Controls (for example, using Vault to manage encryption keys and enforcing encryption of data in block storage, object storage, and other OCI services).</br></br></br></br></br></br> |
| DEPLOY WITH ORM</br> - STEP #1|  [<img src="/commons/images/DeployToOCI.svg"  height="25" align="center">](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/oci-landing-zones/terraform-oci-modules-orchestrator/archive/refs/tags/v2.0.5.zip&zipUrlVariables={"input_config_files_urls":"https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_iam.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_hub_a_network_light.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_observability_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_security_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_governance.auto.tfvars.json"})</br> And follow these steps:</br>1. Accept terms, wait for the configuration to load. </br>2. Set the working directory to “rms-facade”. </br>3. Set the stack name you prefer.</br>4. Set the terraform version to 1.5.x. Click Next. </br>5. Accept the default files. Click Next. Optionally, replace with your json/yaml config files. </br>6. Un-check run apply. Click Create. </br> </br> | [<img src="/commons/images/DeployToOCI.svg"  height="25" align="center">](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/oci-landing-zones/terraform-oci-modules-orchestrator/archive/refs/tags/v2.0.5.zip&zipUrlVariables={"input_config_files_urls":"https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_iam.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_hub_a_network_light.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_observability_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_security_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_governance.auto.tfvars.json"})</br> And follow these steps:</br>1. Accept terms, wait for the configuration to load. </br>2. Set the working directory to “rms-facade”. </br>3. Set the stack name you prefer.</br>4. Set the terraform version to 1.5.x. Click Next. </br>5. Accept the default files. Click Next. Optionally, replace with your json/yaml config files. </br>6. Un-check run apply. Click Create. |






 **DEPLOY WITH ORM** - CIS Level 1 Security Controls 
 


 **DEPLOY WITH ORM** - CIS Level 2 Security Controls   
 
 [<img src="/commons/images/DeployToOCI.svg"  height="25" align="center">](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/oci-landing-zones/terraform-oci-modules-orchestrator/archive/refs/tags/v2.0.5.zip&zipUrlVariables={"input_config_files_urls":"https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_iam.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_hub_a_network_light.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_observability_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_security_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_governance.auto.tfvars.json"}) 