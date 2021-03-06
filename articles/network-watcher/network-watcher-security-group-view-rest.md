---
title: Azure Ağ İzleyicisi güvenlik grubu görünümü - REST API ile ağ güvenlik analiz | Microsoft Docs
description: Bu makalede, bir sanal makine güvenliği'güvenlik grubu görünümü ile çözümlemek için PowerShell kullanmayı anlatmaktadır.
services: network-watcher
documentationcenter: na
author: KumudD
manager: twooley
editor: ''
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: kumud
ms.openlocfilehash: 86fff39605fa91c1b09c1547dd0efa97b8fd26cd
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/13/2019
ms.locfileid: "64687857"
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a>Sanal Makine güvenlik REST API kullanarak güvenlik grubu görünümünü çözümleme

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [Azure CLI](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

Güvenlik grubu görünümü bir sanal makineye uygulanan yapılandırılmış ve etkin ağ güvenlik kuralları döndürür. Bu yetenek, Denetim ve ağ güvenlik grupları ve trafiği okunuyor emin olmak için bir VM üzerinde yapılandırılan kurallardan tanılamak kullanışlıdır doğru bir şekilde izin verilen veya reddedilen. Bu makalede, biz, REST API kullanarak bir sanal makine için etkili ve uygulanan güvenlik kuralları nasıl alınacağını göstermektedir


[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryoda, bir sanal makine için güvenlik grubu görünümünü almak için Ağ İzleyicisi Rest API çağrısı. ARMclient, PowerShell kullanarak REST API'sini çağırmak için kullanılır. ARMClient bulunur, chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)

Bu senaryo, zaten uyguladığınız adımları varsayar [Ağ İzleyicisi oluşturma](network-watcher-create.md) Ağ İzleyicisi oluşturmak için. Senaryo da kullanılacak geçerli bir sanal makine ile bir kaynak grubu var olduğunu varsayar.

## <a name="scenario"></a>Senaryo

Bu makalede ele alınan senaryo, belirli bir sanal makine için etkili ve uygulanan güvenlik kuralları alır.

## <a name="log-in-with-armclient"></a>Oturum ARMClient oturum açın

```powershell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Bir sanal makine alma

Aşağıdaki kod, sanal machineThe döndürmek için aşağıdaki betiği çalıştırın değişkenleri gerekir:

- **Subscriptionıd** -abonelik kimliği ile de alınabilir **Get-AzSubscription** cmdlet'i.
- **resourceGroupName** -sanal makine içeren bir kaynak grubu adı.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Gerekli bilgileri **kimliği** türü altında `Microsoft.Compute/virtualMachines` yanıt, aşağıdaki örnekte görüldüğü gibi:

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a>Sanal makine için güvenlik grubu görünümünü Al

Aşağıdaki örnek, hedeflenen bir sanal makine güvenlik grubu görünümünü ister. Bu örnekte sonuçlar, kuralları ve güvenlik için yapılandırma değişikliklerini aramak için bir kaynak tarafından tanımlanan karşılaştırmak üzere kullanılabilir.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-the-response"></a>Yanıtı görüntüleyin

Aşağıdaki örnek, önceki komuttan döndürülen yanıttır. Gruplar halinde ayrılmış sanal makine üzerindeki tüm etkin ve uygulanan güvenlik kuralları sonuçlarını göster **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, ve  **EffectiveSecurityRules**.

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a>Sonraki adımlar

Ziyaret [denetimi ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-security-group-view-powershell.md) ağ güvenlik gruplarının doğrulama otomatikleştirme hakkında bilgi edinmek için.


