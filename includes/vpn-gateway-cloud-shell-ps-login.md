---
title: include dosyası
description: include dosyası
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 02/01/2019
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: deabef0c2c3540e515fe72a161710c95a20fa86f
ms.sourcegitcommit: 3e98da33c41a7bbd724f644ce7dedee169eb5028
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67188234"
---
PowerShell Konsolunuzu yükseltilmiş ayrıcalıklarla açın.



Azure PowerShell'i yerel olarak çalıştırıyorsanız, Azure hesabınıza bağlanın. *Connect AzAccount* cmdlet için kimlik bilgilerini ister. Azure PowerShell için kullanılabilir olacak şekilde doğrulandıktan sonra hesap ayarlarınızı indirir. PowerShell ile yerel olarak çalışan ve bunun yerine Azure Cloud Shell'i 'Try' tarayıcıda kullanıyorsanız, bu ilk adımı atlayın. Azure hesabınızda otomatik olarak bağlanır.

```azurepowershell
Connect-AzAccount
```

Birden fazla aboneliğiniz varsa, Azure aboneliklerinizin bir listesini alın.

```azurepowershell-interactive
Get-AzSubscription
```

Kullanmak istediğiniz aboneliği belirtin.

```azurepowershell-interactive
Select-AzSubscription -SubscriptionName "Name of subscription"
```