# Azure Load Balancer ARM Template

This ARM template deploys an Azure Load Balancer and configures it to work with existing virtual machines in an Azure environment.

## Prerequisites

- Existing Azure infrastructure deployed using the base infrastructure template
- Two running Virtual Machines
- Virtual Network and Subnet configuration
- Azure CLI or PowerShell installed (for deployment)
- Contributor access to the Azure subscription/resource group

## Resources Deployed

- Standard SKU Load Balancer
- Public IP for Load Balancer (Standard SKU)
- Backend Pool configuration
- Health probe for HTTP
- Load balancing rules for port 80
- Network Interface updates for VM association

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| environment | string | Production | Environment name (must match existing environment) |
| location | string | westeurope | Azure region for deployment |
| removePublicIP | bool | true | Option to remove public IPs from VM NICs |

## Deployment

### Using Azure CLI

```bash
az deployment group create \
  --resource-group <your-resource-group> \
  --template-file lb-template.json \
  --parameters environment=Production
```

### Using PowerShell

```powershell
New-AzResourceGroupDeployment `
  -ResourceGroupName <your-resource-group> `
  -TemplateFile lb-template.json `
  -environment Production
```

## Configuration Details

### Load Balancer
- SKU: Standard
- Frontend: Public IP (Static)
- Backend Pool: Configured for existing VMs
- Health Probe: HTTP:80, 15-second interval
- Rules: Port 80 distribution

### Network Configuration
- Removes public IPs from VMs (optional)
- Adds VMs to backend pool
- Maintains existing subnet associations

## Template Outputs

| Output | Description |
|--------|-------------|
| loadBalancerIP | Public IP address of the Load Balancer |

## Notes

- This template should be deployed after the base infrastructure is in place
- Existing VMs must be running HTTP services on port 80 for health probe
- Public IPs can be optionally retained on VMs using the removePublicIP parameter

## Security Considerations

- Load Balancer provides a single entry point to your application
- VM public IPs can be removed for enhanced security
- NSG rules from base deployment remain in effect
- Standard SKU provides enhanced security features

## Dependencies

This template depends on resources created by the base infrastructure template:
- Virtual Network
- Subnets
- Virtual Machines
- Network Interfaces

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

MIT License

Copyright (c) 2025

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
