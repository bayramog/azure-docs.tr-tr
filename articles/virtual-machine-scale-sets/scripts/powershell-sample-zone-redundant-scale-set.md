---
title: Azure PowerShell Örnekleri - Alanlar arası yedekli ölçek kümesi | Microsoft Docs
description: Azure PowerShell Örnekleri
services: virtual-machine-scale-sets
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/05/2018
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 00dd839c3ef8369490ffdd8840d6d4d8c69c76b5
ms.sourcegitcommit: 943af92555ba640288464c11d84e01da948db5c0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/09/2019
ms.locfileid: "55983891"
---
# <a name="create-a-zone-redundant-virtual-machine-scale-set-with-powershell"></a>PowerShell ile alanlar arası yedekli sanal makine ölçek kümesi oluşturma
Bu betik, birden çok Kullanılabilirlik Alanında Windows Server 2016 çalıştıran bir sanal makine ölçek kümesi oluşturur. Betiği çalıştırdıktan sonra sanal makineye RDP üzerinden erişebilirsiniz.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [updated-for-az-vm.md](../../../includes/updated-for-az-vm.md)]

## <a name="sample-script"></a>Örnek betik

[!code-powershell[main](../../../powershell_scripts/virtual-machine-scale-sets/create-zone-redundant-scale-set/create-zone-redundant-scale-set.ps1 "Create zone-redundant scale set")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme
Kaynak grubunu, ölçek kümesini ve ilgili tüm kaynakları kaldırmak için aşağıdaki komutu çalıştırın.

```powershell
Remove-AzResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Betik açıklaması
Bu betik, dağıtımı oluşturmak için aşağıdaki komutları kullanır. Tablodaki her öğe, komuta özgü belgelere yönlendirir.

| Komut | Notlar |
|---|---|
| [Yeni AzVmss](/powershell/module/az.compute/new-azvmss) | Sanal makine ölçek kümesi ve sanal ağ, yük dengeleyici ve NAT kurallarının dahil olduğu tüm destekleyici kaynakları oluşturur. |
| [Get-AzVmss](/powershell/module/az.compute/get-azvmss) | Sanal makine ölçek kümesi hakkında bilgi alır. |
| [AzVmssExtension ekleyin](/powershell/module/az.compute/add-azvmssextension) | Özel Betik için sanal makine uzantısı ekleyerek temel bir web uygulaması yükler. |
| [Güncelleştirme AzVmss](/powershell/module/az.compute/update-azvmss) | Sanal makine uzantısını uygulamak için sanal makine ölçek kümesi modelini güncelleştirir. |
| [Get-AzPublicIpAddress](/powershell/module/az.network/get-azpublicipaddress) | Yük dengeleyici tarafından kullanılan atanan genel IP adresi hakkında bilgi alır. |
| [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) | Kaynak grubunu ve grubun içerdiği tüm kaynakları kaldırır. |


## <a name="next-steps"></a>Sonraki adımlar
Azure PowerShell modülü hakkında daha fazla bilgi için bkz. [Azure PowerShell belgeleri](/powershell/azure/overview).

Ek sanal makine ölçek kümesi PowerShell betik örnekleri, [Azure sanal makine ölçek kümesi belgelerinde](../powershell-samples.md) bulunabilir.
