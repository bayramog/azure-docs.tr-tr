---
title: Azure PowerShell betiği-Azure Cosmos DB Get üretilen Iş (RU/s) Tablo API'si
description: Azure PowerShell betiği-Azure Cosmos DB Get üretilen Iş (RU/s) Tablo API'si
author: markjbrown
ms.service: cosmos-db
ms.subservice: cosmosdb-table
ms.topic: sample
ms.date: 05/18/2019
ms.author: mjbrown
ms.openlocfilehash: 5d3fa2e2122c006825a8413a2ca2f292bda2de74
ms.sourcegitcommit: 83df2aed7cafb493b36d93b1699d24f36c1daa45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2019
ms.locfileid: "71178704"
---
# <a name="get-throughput-rus-for-a-table-for-azure-cosmos-db---table-api"></a>Azure Cosmos DB Tablo API'si için bir tablo için üretilen Iş (RU/sn) Al

[!INCLUDE [updated-for-az](../../../../../includes/updated-for-az.md)]

[!INCLUDE [sample-powershell-install](../../../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>Örnek betik

[!code-powershell[main](../../../../../powershell_scripts/cosmosdb/table/ps-table-ru-get.ps1 "Get throughput on a table for Table API")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Betik örneği çalıştırıldıktan sonra, kaynak grubunu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komut kullanılabilir.

```powershell
Remove-AzResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Betik açıklaması

Bu betik aşağıdaki komutları kullanır. Tablodaki her komut, komuta özgü belgelere yönlendirir.

| Komut | Notlar |
|---|---|
|**Azure kaynakları**| |
| [New-AzResource](https://docs.microsoft.com/powershell/module/az.resources/new-azresource) | Bir kaynak oluşturur. |
|**Azure Kaynak grupları**| |
| [Remove-AzResourceGroup](https://docs.microsoft.com/powershell/module/az.resources/remove-azresourcegroup) | Bir kaynak grubunu tüm iç içe geçmiş kaynaklar dahil siler. |
|||

## <a name="next-steps"></a>Sonraki adımlar

Azure PowerShell hakkında daha fazla bilgi için bkz. [Azure PowerShell belgeleri](https://docs.microsoft.com/powershell/).

Ek Azure Cosmos DB PowerShell betiği örnekleri, [Azure Cosmos DB PowerShell betiklerinde](../../../powershell-samples.md) bulunabilir.