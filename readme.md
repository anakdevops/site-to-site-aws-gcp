# Site-to-Site VPN Configuration between AWS and GCP

---

## AWS Configuration (Prod)

### Create VPC
- **Choose VPC and more**
- **Name**: `aws-vpc-hybrid-prod`  
- **IPv4 CIDR block**: `10.0.0.0/16`
- **Number of Availability Zones (AZs)** : 2
- **Number of public subnets** : 2
- **Number of private subnets** : 2

## GCP Configuration (Dev)

### VPC
- **Name**: `gcp-vpc-hybrid-dev`

### Subnets
- **Public Subnet**: `gcp-vpc-hybrid-public-subnet-dev`  
  - CIDR: `11.0.1.0/24`
- **Private Subnet**: `gcp-vpc-hybrid-private-subnet-dev`  
  - CIDR: `11.0.2.0/24`
 
## Create VM on AWS & GCP
- test ping

## AWS Configuration (Prod)

### Customer Gateways (GCP IPs)
- `aws-vpc-hybrid-cgw-1-prod`  
  - ASN: `65412`  
  - IP: _From GCP_
- `aws-vpc-hybrid-cgw-2-prod`  
  - ASN: `65412`  
  - IP: _From GCP_

### Virtual Private Gateway
- **Name**: `aws-vpc-hybrid-vpgw-prod`  
- **ASN**: `65413`

### Site-to-Site VPN Connections
- `aws-vpc-hybrid-vpn01-prod`
- `aws-vpc-hybrid-vpn02-prod`
- **Configuration Download**:  
  - **Vendor**: Generic  
  - **Protocol**: IKEv2
 
### Enable route propagation
- **Edit route table** : enable propagation

---

## GCP Configuration (Dev)

### Cloud Router
- **Name**: `gcp-aws-router-cloud-dev`  
- **ASN**: `65412`

### HA VPN Gateway
- **Name**: `aws-gcp-vpn-gateway-dev`

### Peer VPN Configuration
- **Peer Name**: `gcp-aws-peer-vpn-dev`  
- **Interfaces**: 4
- Copy Virtual Private Gateway
- **Authentication**: Input pre-shared key from AWS Site-to-Site VPN configuration
- **Create bgp** : ASN & IP from AWS Site-to-Site VPN configuration
- Copy Inside IP Addresses
---

