---
title: Azure PowerShell betik örneği-Azure PowerShell birden çok Web sitesinin yükünü dengeleme | Microsoft Docs
description: Azure PowerShell betik örneği-aynı sanal makineye birden çok Web sitesinin yükünü dengeleme
services: load-balancer
documentationcenter: load-balancer
author: asudbring
manager: KumudD
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: allensu
ms.openlocfilehash: 0b266f5fcad0ef709e29a125f1b9b5ddba7fec90
ms.sourcegitcommit: cf36df8406d94c7b7b78a3aabc8c0b163226e1bc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/09/2019
ms.locfileid: "73890298"
---
# <a name="load-balance-multiple-websites"></a>Birden çok Web sitesinin yükünü dengelemek

Bu betik örneği, bir kullanılabilirlik kümesinin üyesi olan iki sanal makineye (VM) sahip bir sanal ağ oluşturur. Yük dengeleyici iki ayrı IP adresi için trafiği iki VM’ye yönlendirir. Betiği çalıştırdıktan sonra, web sunucusu yazılımını VM’lere dağıtabilir ve her biri kendi IP adresine sahip birden fazla web sitesi barındırabilirsiniz.

Gerekirse, [Azure PowerShell kılavuzunda](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) bulunan yönergeleri kullanarak Azure PowerShell’i yükleyin ve ardından Azure ile bağlantı oluşturmak için `Connect-AzAccount` komutunu çalıştırın.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek betik

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Kaynak grubunu, VM’yi ve ilgili tüm kaynakları kaldırmak için aşağıdaki komutu çalıştırın.

```powershell
Remove-AzResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Betik açıklaması

Bu betik bir kaynak grubu, sanal ağ, yük dengeleyici ve tüm ilgili kaynakları oluşturmak için aşağıdaki komutları kullanır. Tablodaki her komut, komuta özgü belgelere yönlendirir.

| Komut | Notlar |
|---|---|
| [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup) | Tüm kaynakların depolandığı bir kaynak grubu oluşturur. |
| [New-AzAvailabilitySet](/powershell/module/az.compute/new-azavailabilityset) | Yüksek oranda kullanılabilirlik sağlamak için bir Azure kullanılabilirlik kümesi oluşturur. |
| [New-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/new-azvirtualnetworksubnetconfig) | Bir alt ağ yapılandırması oluşturur. Bu yapılandırma, sanal ağ oluşturma işlemiyle birlikte kullanılır. |
| [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) | Sanal ağ oluşturur. |
| [New-Azpublicıpaddress](/powershell/module/az.network/new-azpublicipaddress) | Genel bir IP adresi oluşturur. |
| [New-Azloadbalancerfrontendıpconfig](/powershell/module/az.network/new-azloadbalancerfrontendipconfig) | Yük dengeleyici için bir ön uç IP yapılandırması oluşturur. |
| [New-Azloadbalancerbackendadddresspoolconfig](/powershell/module/az.network/new-azloadbalancerbackendaddresspoolconfig) | Yük dengeleyici için bir arka uç adres havuzu yapılandırması oluşturur. |
| [New-AzLoadBalancerProbeConfig](/powershell/module/az.network/new-azloadbalancerprobeconfig) | Bir NLB araştırması oluşturur. NLB araştırması, NLB kümesindeki her bir VM’yi izlemek için kullanılır. Herhangi bir VM erişilemez hale gelirse trafik VM’ye yönlendirilmez. |
| [New-AzLoadBalancerRuleConfig](/powershell/module/az.network/new-azloadbalancerruleconfig) | Bir NLB kuralı oluşturur. Bu örnekte 80 numaralı bağlantı noktası için bir kural oluşturulur. HTTP trafiği NLB’ye ulaştığında, NLB kümesindeki VM’lerden birinin 80 numaralı bağlantı noktasına yönlendirilir. |
| [New-AzLoadBalancer](/powershell/module/az.network/new-azloadbalancer) | Yük dengeleyici oluşturur. |
| [New-Aznetworkınterfaceipconfig](/powershell/module/az.network/new-aznetworkinterfaceipconfig) | Bir sanal ağ arabirimi için gelişmiş özellikleri tanımlar. |
| [New-Aznetworkınterface](/powershell/module/az.network/new-aznetworkinterface) | Ağ arabirimi oluşturur. |
| [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig) | Sanal makine yapılandırması oluşturur. Bu yapılandırma; sanal makine adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir. Yapılandırma, sanal makine oluşturulurken kullanılır. |
| [New-AzVM](/powershell/module/az.compute/new-azvm) | Sanal makine oluşturur. |
|[Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) | Kaynak grubunu ve grubun içerdiği tüm kaynakları kaldırır. |

## <a name="next-steps"></a>Sonraki adımlar

Azure PowerShell hakkında daha fazla bilgi için bkz. [Azure PowerShell belgeleri](https://docs.microsoft.com/powershell/azure/overview).

Ek ağ PowerShell betiği örnekleri, [Azure Ağına Genel Bakış belgeleri](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json) içinde bulunabilir.
