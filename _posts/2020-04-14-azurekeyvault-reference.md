---
layout: post
title: Reference Azure keyvault in ARM parameter file
date: 2020-04-14 16:50
category:
author:
tags: []
summary:
---
It is always best practice to use some key vault service when using ARM templates.

In our example, I am using Azure key vault service

Steps -

* Assuming you have the azuredeploy or any other name template file and parameter file. If you do not have one use the Azure quickstart template as a reference.

* Login to Azure portal, search for Key vault and create a new one

![an image alt text]({{ https://github.com/AshwanthTiwari/tiwarilabs.github.io }}/images/azure-keyvault1.png "an image title")

or using
PowerShell

`New-AzKeyVault -Name 'MykeyVault' -ResourceGroupName 'MyResourceGroup' -Location 'Australia East'`

* Once key vault is ready, create a new secret.

![an image alt text]({{ https://github.com/AshwanthTiwari/tiwarilabs.github.io }}/images/azure-keyvault2.png "an image title")
or using Powershell

```azurepowershell

$secretvalue = ConvertTo-SecureString 'somesecret' -AsPlainText -Force
$secret = Set-AzKeyVaultSecret -VaultName 'MykeyVault' -Name 'ExamplePassword' -SecretValue $secretvalue
(Get-AzKeyVaultSecret -vaultName "MykeyVault" -name "ExamplePassword").SecretValueText

```

* Click Properties under key vault to obtain the Resource ID

![an image alt text]({{ https://github.com/AshwanthTiwari/tiwarilabs.github.io }}/images/azure-keyvault3.png "an image title")

* Now, you have the required the information. Open the ARM parameters JSON file using VSCode or any other editor.

![an image alt text]({{ https://github.com/AshwanthTiwari/tiwarilabs.github.io }}/images/azure-keyvault4.png "an image title")


```json
   "adminPassword": {
            "reference": {
                "keyvault":{
                    "id": "Resource ID obtained from step 4 eg. /subscription/229xxxxxxxx/resourceGroups/rgname/providers/Microsoft.keyvaults/vaults/keyvaultname"
                },
                "secretName": "winpass"
            }
        },
```
* Last step, this can be enabled before as well. In Azure Portal, ensure enable access to templates is checked.

This can be found under key vaults-->Access Policies

![an image alt text]({{ https://github.com/AshwanthTiwari/tiwarilabs.github.io }}/images/azure-keyvault5.png "an image title")








