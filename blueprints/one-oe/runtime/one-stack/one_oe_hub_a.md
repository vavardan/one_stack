 
 # **One-OE + Hub A: One-Stack Deployment**
 
 ### Overview
 This document provides a detailed overview of the One-OE Landing Zone with Hub A addon, including its components and deployment guidance.

 ### Deployment Diagram
 

 ### Input Configurations

| JSON configuration | Configuration-defined components | Terraform module | 
|:-|:-|:-|
| [**IAM Configuration**](oci_open_lz_one-oe_iam.auto.tfvars.json) | Compartments, Identity Domain, IAM groups, policies | [OCI Landing Zone IAM](https://github.com/oci-landing-zones/terraform-oci-modules-iam) |
| [**Network Configuration**](oci_open_lz_hub_a_network_light.auto.tfvars.json) | Hub A, two OCI Network Firewalls (DMZ, Internal), Internet GW, NAT GW, Service GW, DRG, Routing tables, two Spoke VCNs (Prod, PreProd) Security Lists, NSGs| [OCI Landing Zone Network](https://github.com/oci-landing-zones/terraform-oci-modules-networking) |
| [**Security Configuration**](oci_open_lz_one-oe_security_cisl1.auto.tfvars.json) | Security Zones, Cloud Guard | [OCI Landing Zone Security](https://github.com/oci-landing-zones/terraform-oci-modules-security) |
| [**Observability Configuration**](oci_open_lz_one-oe_observability_cisl1.auto.tfvars.json) | Events, Alarms, Logging, and Notifications | [OCI Landing Zone Observability](https://github.com/oci-landing-zones/terraform-oci-modules-observability) |



 
 **DEPLOY WITH ORM** - CIS Level 1 Security Controls 
 
 [<img src="/commons/images/DeployToOCI.svg"  height="25" align="center">](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/oci-landing-zones/terraform-oci-modules-orchestrator/archive/refs/tags/v2.0.5.zip&zipUrlVariables={"input_config_files_urls":"https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_iam.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_hub_a_network_light.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_observability_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_security_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_governance.auto.tfvars.json"}) 

 **DEPLOY WITH ORM** - CIS Level 2 Security Controls   
 
 [<img src="/commons/images/DeployToOCI.svg"  height="25" align="center">](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/oci-landing-zones/terraform-oci-modules-orchestrator/archive/refs/tags/v2.0.5.zip&zipUrlVariables={"input_config_files_urls":"https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_iam.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_hub_a_network_light.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_observability_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_security_cisl1.auto.tfvars.json,https://raw.githubusercontent.com/oci-landing-zones/oci-landing-zone-operating-entities/master/blueprints/one-oe/runtime/one-stack/oci_open_lz_one-oe_governance.auto.tfvars.json"}) 