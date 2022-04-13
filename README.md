# Ansible_ISE_Policy_Set_MM_LIM
Ansible playbook for creating Wired Monitor Mode &amp; Low Impact Mode Policy Sets in Cisco Identity Services Engine (ISE) 3.1+

## ISE Pre-requisites
The following ISE configurations are required prior to running this playbook:

1. An administrator account with the 'ERS Admin' role
2. An Active Directory Join Point configured and the AD Groups 'Domain Computers' and 'Domain Users' added

## Policies and Policy Elements created
The following Policy Elements and Policy Sets are created by this playbook:

### Policy Elements

 - Allowed Protocols list named 'MAB_Dot1x' with the following protocols enabled:
   - Process Host Lookup (MAB)
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
   - Dot1x PEAP
   - MAB
 - AuthZ Policies
   - AD User and Computer (EAP Chaining)
   - AD Users
   - AD Computers
   - Default (updated AuthZ Profile)

Wired_LIM
 - AuthC Policies
   - Dot1x Certificate
   - Dot1x PEAP
   - MAB
 - AuthZ Policies
   - AD User and Computer (EAP Chaining)
   - AD Users
   - AD Computers
   - Default (updated AuthZ Profile)

## Ansible Pre-requisites
Running this playbook requires Python and Ansible software installed.
If you have any problems installing Python or Ansible, see [Installing Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

Using Ansible to interact with the Cisco ISE API also requires the Cisco ISE SDK and Ansible Collection.
See [Ansible Modules for Cisco ISE](https://galaxy.ansible.com/cisco/ise) for more information.

## Quick Start
1. Clone this repository:  

    ```bash
    git clone https://github.com/grg1bbs/Ansible_ISE_Policy_Set_MM_LIM
    ```
 
2. Edit the 'credentials.yml' and 'hosts' file to suit your environment

3. Edit the 'policyset-mm-lim.yml' file to replace the <my_domain_name> and <my_join_point_name> variables with the values used in your ISE deployment

4. Run the Ansible playbook

    ```bash
    ansible-playbook -i hosts policyset-mm-lim.yml
    ```
