# create Bash shell variables

vnetName=TestVNet1
subnetName=TestSubnet1
vnetAddressPrefix=10.0.0.0/16
subnetAddressPrefix=10.0.0.0/24

# Use the existing resource group
resourceGroup=RG_AV_Resources

az network vnet create 
--name $vnetName 
--resource-group $resourceGroup 
--address-prefixes $vnetAddressPrefix 
--subnet-name $subnetName 
--subnet-prefixes $subnetAddressPrefix


# create Bash shell variable
vmName=AV_VM1w

az vm create \
  --resource-group $resourceGroup \
  --name $vmName \
  --image Ubuntu2204 \
  --storage-sku Standard_LRS \
  --vnet-name $vnetName \
  --subnet $subnetName \
  --generate-ssh-keys \
  --output json \
  --verbose

#ssh to VM 
ssh -i <private-key-file> user@host

#for delete all resources and resource group

az group delete --name nameofresourcegroup
