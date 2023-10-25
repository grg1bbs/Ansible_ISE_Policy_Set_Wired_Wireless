# Ansible_ISE_Policy_Set_Wired_Wireless
Ansible playbook for creating Wired Monitor Mode, Wired Low Impact Mode, and Wireless Secure Policy Sets in Cisco Identity Services Engine (ISE) 3.1+

This playbook was validated using:
 - ISE 3.1 patch 7
 - Ansible 2.15.5
 - CiscoISESDK 2.0.12
 - ISE Ansible collection 2.5.16

## ISE Pre-requisites
The following ISE configurations are required prior to running this playbook:

 1. An administrator account with the 'ERS Admin' role
 2. An Active Directory domain admin account with Join permissions

## Policies and Policy Elements created
The following Policy Elements and Policy Sets are created by this playbook:

### Policy Elements

 - Active Directory Join Point
   - Join node(s) to domain in the defined Org Unit
   - Add default 'Domain Users' and Domain Computers' AD groups
 - Allowed Protocols list named 'MAB_Dot1x' with the following protocols enabled:
   - Process Host Lookup (MAB)
   - EAP-TLS
   - PEAP(MSCHAPv2)
   - TEAP (MSCHAPv2 & EAP-TLS inner methods) with EAP Chaining
 - Allowed Protocols list named 'Dot1x' with the following protocols enabled:
   - EAP-TLS
   - PEAP(MSCHAPv2)
   - TEAP (MSCHAPv2 & EAP-TLS inner methods) with EAP Chaining
 - Certificate Authentication Profile (for EAP-TLS)
 - Identity Source Sequence with CAP & AD
 - Network Device Group (NDG) structure for Monitor Mode & Low Impact Mode
 - Downloadable ACLs and AuthZ Profiles
   - Permissive DACLs (permit ip any any) except for LIM Default (permits DHCP, DNS, and TFTP only)

### Policy Sets

Wired_MM
 - AuthC Policies
   - Dot1x Certificate
   - MAB
 - AuthZ Policies
   - AD User and Computer (EAP Chaining)
   - AD Users
   - AD Computers
   - Default (updated AuthZ Profile)

Wired_LIM
 - AuthC Policies
   - Dot1x Certificate
   - MAB
 - AuthZ Policies
   - AD User and Computer (EAP Chaining)
   - AD Users
   - AD Computers
   - Default (updated AuthZ Profile)

Wireless Secure
 - AuthC Policies
   - Dot1x Certificate
 - AuthZ Policies
   - AD User and Computer (EAP Chaining)
   - AD Users
   - AD Computers

## Ansible Pre-requisites
Running this playbook requires Python and Ansible software installed.
If you have any problems installing Python or Ansible, see [Installing Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

Using Ansible to interact with the Cisco ISE API also requires the Cisco ISE SDK and Ansible Collection.
See [Ansible Modules for Cisco ISE](https://galaxy.ansible.com/cisco/ise) for more information.

## Quick Start
1. Clone this repository:  

    ```bash
    git clone https://github.com/grg1bbs/Ansible_ISE_Policy_Set_Wired_Wireless
    ```
 
2. Edit the following files to suit your environment:
 - credentials.yaml
 - hosts
 - variables.yaml

4. Run the Ansible playbook

    ```bash
    ansible-playbook -i hosts policyset.yaml
    ```
