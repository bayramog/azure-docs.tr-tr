---
author: rayne-wiselman
ms.service: site-recovery
ms.topic: include
ms.date: 10/26/2018
ms.author: raynew
ms.openlocfilehash: 96cba4e077be8b7658c270b09b177a845e16c8b0
ms.sourcegitcommit: 3e98da33c41a7bbd724f644ce7dedee169eb5028
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67188897"
---
Bu makalede aşağıdaki durumlar varsayılır

1. Şirket içi ağınız ile Azure Sanal Ağ arasında **Siteden Siteye VPN** veya **Express Route** bağlantısı zaten oluşturulmuştur.
2. Kullanıcı hesabınız sanal makinelerin yük devrettiği Azure Aboneliğinde yeni bir sanal makine oluşturma izinlerine sahiptir.
3. Aboneliğinizde, yeni bir İşlem Sunucusu sanal makinesi çalıştırabilecek en az 4 Çekirdek vardır.
4. **Configuration Server Parolanız** mevcuttur.

> [!TIP]
> Sanal makinelerin yük devrettiği Azure Sanal Ağından Configuration Server (şirket içinde çalışan) 443 bağlantı noktasını bağlayabildiğinizden emin olun.
