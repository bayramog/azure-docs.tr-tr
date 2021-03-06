---
title: VM başına Azure vCPU kotası artış istekleri | Microsoft Docs
description: VM başına vCPU kota artışı istekleri
author: sowmyavenkat86
ms.author: svenkat
ms.date: 06/07/2019
ms.topic: article
ms.service: azure-supportability
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: e99bdd92d4a1aab833a95943b22aaabe7f0daa1d
ms.sourcegitcommit: 961468fa0cfe650dc1bec87e032e648486f67651
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72248671"
---
# <a name="vm-series-vcpu-limit-increase"></a>VM Serisi vCPU sınırı artışı

Sanal makineler ve sanal makine ölçek kümeleri için Kaynak Yöneticisi vCPU kotaları, her bir bölgede her bir abonelik için iki katmanda zorlanır. 

İlk katman **Toplam bölgesel vCPU sayısı sınırı** (tüm VM serileri genelinde) ve ıkıncı katman **VM Serisi vCPU sayısı sınırı** (D serisi vCPU 'lar gibi). Yeni bir VM 'nin dağıtılması her seferinde, bu VM Serisi için yeni ve var olan vCPU 'ların toplamı, söz konusu VM Serisi için onaylanan vCPU kotasını aşmamalıdır. Ayrıca, tüm VM dizileri genelinde dağıtılan toplam yeni ve var olan vCPU sayısı, abonelik için onaylanan toplam bölgesel vCPU kotasını aşmamalıdır. Bu kotalardan biri aşılırsa, VM dağıtımına izin verilmez.
Azure portal VM Serisi için vCPU kota sınırı artışı isteyebilirsiniz. VM Serisi kotasının bir artışı toplam bölgesel vCPU sayısını aynı tutara göre otomatik olarak arttırır. 

[Sanal makine vCPU kotaları sayfasında](https://docs.microsoft.com/azure/virtual-machines/windows/quotas) ve [Azure aboneliği ve hizmet limitleri](https://aka.ms/quotalimits) sayfasında kotalar hakkında daha fazla bilgi edinin. 

Artık **Yardım + Destek** dikey penceresi veya portalda **kullanımlar + kota** dikey penceresi aracılığıyla bir artış isteğinde bulunabilir. 

## <a name="request-per-vm-series-vcpu-quota-increase-at-subscription-level-using-the-help--support-blade"></a>**Yardım + Destek** dikey penceresini kullanarak ABONELIK düzeyindeki VM Serisi vCPU kotası artışına göre istek

Azure portal Azure 'un ' yardım + destek ' dikey penceresi aracılığıyla bir destek isteği oluşturmak için aşağıdaki yönergeleri izleyin. 

1. @No__t-0 ' dan **Yardım + Destek**' i seçin.

   ![Yardım ve destek](./media/resource-manager-core-quotas-request/helpsupport.png)
 
2.  **Yeni destek isteği ' ni**seçin. 

     ![Yeni destek isteği](./media/resource-manager-core-quotas-request/newsupportrequest.png)

3. Sorun türü açılır listesinde **hizmet ve abonelik limitleri (kotalar)** öğesini seçin.

   ![Sorun türü açılan kutusu](./media/resource-manager-core-quotas-request/issuetypedropdown.png)

4. Daha fazla kotanın olması gereken aboneliği seçin.

   ![Abonelik newSR 'yi seçin](./media/resource-manager-core-quotas-request/select-subscription-sr.png)
   
5. **Kota türü** açılan menüsünde **işlem-VM (çekirdek-vCPU) abonelik sınırı artışları** ' ni seçin. 

   ![Kota türünü seçin](./media/resource-manager-core-quotas-request/select-quota-type.png)

6. **Sorun ayrıntıları**' nda, **Ayrıntılar sağla**' ya tıklayarak isteğinizi işlemeye yardımcı olacak ek bilgiler sağlayın.

   ![Ayrıntıları belirtin](./media/resource-manager-core-quotas-request/provide-details.png)

7. **Kota ayrıntıları** panelinde, dağıtım modeli ' ni seçin ve bir konum seçin.

   ![Kota ayrıntıları DM](./media/resource-manager-core-quotas-request/quota-details.png)

8. Artış gerektiren **SKU aileleri** seçin. 

   ![SKU ailesi](./media/resource-manager-core-quotas-request/sku-family.png)

9. Abonelikte istediğiniz yeni limitleri girin. Bir satırı kaldırmak için, SKU ailesi açılan menüsünden SKU 'nun işaretini kaldırın veya atma "x" simgesine tıklayın. Her SKU ailesi için istenen kotayı girdikten sonra, destek isteği oluşturmaya devam etmek için kota ayrıntıları panelinde **Kaydet ve devam et** ' e tıklayın.

   ![Yeni sınırlar](./media/resource-manager-core-quotas-request/new-limits.png)


## <a name="request-per-vm-series-vcpu-quota-increase-at-subscription-level-using-usages--quota-blade"></a>**Kullanımlar + kota** dikey penceresini kullanarak abonelik düzeyindeki sanal makine serisi vCPU kotası artışına göre istek

Azure 'un ' kullanım + kota ' dikey penceresi aracılığıyla Azure portal kullanılabilir bir destek isteği oluşturmak için aşağıdaki yönergeleri izleyin. 

1. @No__t-0 ' dan **abonelikler**' i seçin.

   ![Abonelikler](./media/resource-manager-core-quotas-request/subscriptions.png)

2. Daha fazla kotanın olması gereken aboneliği seçin.

   ![Abonelik seçin](./media/resource-manager-core-quotas-request/select-subscription.png)

3. **Kullanım + kotalar** ' ı seçin

   ![Kullanım ve kotaları seçin](./media/resource-manager-core-quotas-request/select-usage-quotas.png)

4. Sağ üst köşede **istek artışı**' nı seçin.

   ![İstek artışı](./media/resource-manager-core-quotas-request/request-increase.png)

5. **İşlem-VM (çekirdek-vCPU) abonelik sınırı** ' nı seçin, teklif türü olarak artar. 

   ![Formu doldur](./media/resource-manager-core-quotas-request/select-quota-type.png)
   
6. **Kota ayrıntıları** panelinde, dağıtım modeli ' ni seçin ve bir konum seçin.

   ![Kota sorunu dikey penceresi](./media/resource-manager-core-quotas-request/quota-details.png)

7. Artış gerektiren **SKU aileleri** seçin.

   ![SKU serisi seçildi](./media/resource-manager-core-quotas-request/sku-family.png)

8. Abonelikte istediğiniz yeni limitleri girin. Bir satırı kaldırmak için, SKU ailesi açılan menüsünden SKU 'nun işaretini kaldırın veya atma "x" simgesine tıklayın. Her SKU ailesi için istenen kotayı girdikten sonra, destek isteği oluşturmaya devam etmek için sorun adımı sayfasında Kaydet ' e tıklayın **ve devam edin** .

   ![SKU yeni kota isteği](./media/resource-manager-core-quotas-request/new-limits.png)
 
