---
layout: default
title: Azure DNS Zones
date created: 2020-07-09T21:27:39.000Z
categories: Azure update
author: joseph
---
# Azure DNS Zones
2020-07-09 21:27:39

Source: 
<https://docs.microsoft.com/en-us/azure/dns/private-dns-getstarted-powershell>

```powershell
Install-Module -Name Az.PrivateDns -force

$backendSubnet = New-AzVirtualNetworkSubnetConfig -Name backendSubnet -AddressPrefix "10.2.0.0/24"
$vnet = New-AzVirtualNetwork `
-ResourceGroupName MyAzureResourceGroup `
-Location eastus `
-Name myAzureVNet `
-AddressPrefix 10.2.0.0/16 `
-Subnet $backendSubnet

$zone = New-AzPrivateDnsZone -Name private.contoso.com -ResourceGroupName MyAzureResourceGroup

$link = New-AzPrivateDnsVirtualNetworkLink -ZoneName private.contoso.com `
-ResourceGroupName MyAzureResourceGroup -Name "mylink" `
-VirtualNetworkId $vnet.id -EnableRegistration
```
## create new dns record
```powershell
New-AzPrivateDnsRecordSet -Name db -RecordType A -ZoneName private.contoso.com `
-ResourceGroupName MyAzureResourceGroup -Ttl 3600 `
-PrivateDnsRecords (New-AzPrivateDnsRecordConfig -IPv4Address "10.2.0.4")
```

EOF
