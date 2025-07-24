**Infrastructure Deployment**
# Overview
ARM template that deploys a Windows Server 2019 Domain Controller and Windows 10 client in an isolated Azure virtual network for Active Directory lab environments.

## TL;DR
Update variables in `template.json` before deployment! This is a test lab environment - beef up security controls for production use.

## Resources Created
- Virtual Network: YOUR-VNET-NAME-HERE (10.0.0.0/16)
- Subnet: YOUR-SUBNET-NAME-HERE (10.0.0.0/24)
- Windows Server 2019 VM: Domain Controller role
- Windows 10 Pro VM: Domain member client
- Network Security Groups: RDP access (port 3389)
- Public IP Addresses: Dynamic allocation for remote access
- Network Interfaces: Connected to subnet

## Template Customization
**BEFORE DEPLOYMENT**
<br></br>
Edit `template.json` and update the variables with your preferred values

## Optional Customizations
You can also modify:
- VM sizes (currently Standard_DS2_v2)
- Network address spaces (currently 10.0.0.0/16)

## Required Pipeline Variables - Note: DO NOT HARDCODE PASSWORDS
- `adminUsername`: Local admin username for both VMs
- `winServerAdminPassword`: Secure password for Windows Server
- `win10AdminPassword`: Secure password for Windows 10 VM

## Security Notes
- NSGs currently allow RDP from any source (0.0.0.0/0)
- For production use, **restrict source IP ranges**
- Change default passwords immediately after deployment
- Consider using Azure Bastion for more secure access

## Troubleshooting
Common Issues:
- Deployment fails: Check Azure region availability for VM sizes
- RDP connection fails: Verify NSG rules and VM is running
- VMs can't communicate: Ensure both are in same subnet (should be automatic)

## Template Specifications
- ARM Template Version: 2019-04-01
- VM Size: Standard_DS2_v2 (2 vCPUs, 7GB RAM)
- Storage: Premium SSD managed disks
- Operating Systems:
  - Windows Server 2019 Datacenter
  - Windows 10 Pro 22H2
 
## Next Steps
- Implement enhanced security controls and network segmentation
  - RDP IP restrictions: limiting RDP access to specific IP ranges instead of 0.0.0.0/0 
- Deploy Multi-Factor Authentication (MFA) for user accounts
- Add monitoring and logging for security compliance
