  az group create --name chmurowiskoRG --location westeurope
az vmss create \
  --resource-group chmurowiskoRG \
  --name chmurowiskoSC \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --admin-username azureuser \
  --generate-ssh-keys

{
  "vmss": {
    "overprovision": true,
    "provisioningState": "Succeeded",
    "singlePlacementGroup": true,
    "uniqueId": "f87c6344-5ce2-4bc6-8bb2-0266e8facdc9",
    "upgradePolicy": {
      "mode": "Automatic"
    },
    "virtualMachineProfile": {
      "networkProfile": {
        "networkInterfaceConfigurations": [
          {
            "name": "chmurdcbfNic",
            "properties": {
              "dnsSettings": {
                "dnsServers": []
              },
              "enableAcceleratedNetworking": false,
              "enableIPForwarding": false,
              "ipConfigurations": [
                {
                  "name": "chmurdcbfIPConfig",
                  "properties": {
                    "loadBalancerBackendAddressPools": [
                      {
                        "id": "/subscriptions/d4684df1-4f8e-489d-8156-ad2fc9bfc0b3/resourceGroups/chmurowiskoRG/providers/Microsoft.Network/loadBalancers/chmurowiskoSCLB/backendAddressPools/chmurowiskoSCLBBEPool",
                        "resourceGroup": "chmurowiskoRG"
                      }
                    ],
                    "loadBalancerInboundNatPools": [
                      {
                        "id": "/subscriptions/d4684df1-4f8e-489d-8156-ad2fc9bfc0b3/resourceGroups/chmurowiskoRG/providers/Microsoft.Network/loadBalancers/chmurowiskoSCLB/inboundNatPools/chmurowiskoSCLBNatPool",
                        "resourceGroup": "chmurowiskoRG"
                      }
                    ],
                    "privateIPAddressVersion": "IPv4",
                    "subnet": {
                      "id": "/subscriptions/d4684df1-4f8e-489d-8156-ad2fc9bfc0b3/resourceGroups/chmurowiskoRG/providers/Microsoft.Network/virtualNetworks/chmurowiskoSCVNET/subnets/chmurowiskoSCSubnet",
                      "resourceGroup": "chmurowiskoRG"
                    }
                  }
                }
              ],
              "primary": true
            }
          }
        ]
      },
      "osProfile": {
        "adminUsername": "azureuser",
        "allowExtensionOperations": true,
        "computerNamePrefix": "chmurdcbf",
        "linuxConfiguration": {
          "disablePasswordAuthentication": true,
          "provisionVMAgent": true,
          "ssh": {
            "publicKeys": [
              {
                "keyData": "ssh-rsa 
                "path": "/home/azureuser/.ssh/authorized_keys"
              }
            ]
          }
        },
        "secrets": []
      },
      "storageProfile": {
        "imageReference": {
          "offer": "UbuntuServer",
          "publisher": "Canonical",
          "sku": "16.04-LTS",
          "version": "latest"
        },
        "osDisk": {
          "caching": "ReadWrite",
          "createOption": "FromImage",
          "managedDisk": {
            "storageAccountType": "Premium_LRS"
          }
        }
      }
    }
  }
}
