# Azure-ARM-Templates

This repository contains Azure Resource Manager (ARM) templates for deploying and managing Azure infrastructure. The templates are designed to work together to create a complete web application environment with load balancing capabilities.

## Repository Structure

```
Azure-ARM-Templates/
├── Base-Infrastructure/        # Base infrastructure deployment
│   ├── VNet-VM-Template.json
│   └── Base-Infrastructure.md
├── Load-Balancer/             # Load Balancer deployment
│   ├── LB-Template.json
│   └── LB-Template.md
└── README.md                  # This file
```

## Templates Overview

### Base Infrastructure Template
- Creates a complete web application infrastructure
- Deploys Virtual Network with subnets
- Creates two Ubuntu web servers in an availability set
- Configures Network Security Groups
- Sets up Public IPs and Network Interfaces
- [More details](./Base-Infrastructure/Base-Infrastructure.md)

### Load Balancer Template
- Deploys an Azure Load Balancer
- Configures backend pool with existing VMs
- Sets up health probes and load balancing rules
- Option to remove public IPs from VMs
- [More details](./Load-Balancer/LB-Template.md)

## Deployment Order

1. Deploy the base infrastructure template first
2. Deploy the load balancer template second

## Prerequisites

- Azure subscription
- Azure CLI or PowerShell installed
- Contributor access to target subscription/resource group
- Basic understanding of Azure networking concepts

## Quick Start

1. Clone this repository:
```bash
git clone https://github.com/yourusername/Azure-ARM-Templates.git
cd Azure-ARM-Templates
```

2. Deploy base infrastructure:
```bash
az deployment group create \
  --resource-group <your-resource-group> \
  --template-file Base-Infrastructure/VNet-VM-Template.json \
  --parameters environment=Production
```

3. Deploy load balancer:
```bash
az deployment group create \
  --resource-group <your-resource-group> \
  --template-file Load-Balancer/LB-Template.json \
  --parameters environment=Production
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## Security

These templates implement several security best practices:
- Network Security Groups with restricted access
- Option for private-only VM access
- Standard SKU Load Balancer
- Configurable environmental parameters

## License

This project is licensed under the MIT License - see the individual template folders for license details.
