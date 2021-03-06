---
title: Azure Service Fabric uygulama ve küme en iyi uygulamalar | Microsoft Docs
description: Service Fabric kümeleri ve uygulamaları yönetmek için en iyi yöntemler.
services: service-fabric
documentationcenter: .net
author: peterpogorski
manager: chackdan
editor: ''
ms.assetid: 19ca51e8-69b9-4952-b4b5-4bf04cded217
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/18/2019
ms.author: pepogors
ms.openlocfilehash: 5fdbd3f15b11e4c3975ca29627d5984382bcf049
ms.sourcegitcommit: b7a44709a0f82974578126f25abee27399f0887f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67206796"
---
# <a name="azure-service-fabric-application-and-cluster-best-practices"></a>Azure Service Fabric uygulama ve küme için en iyi yöntemler

Bu makalede, Azure Service Fabric uygulama ve kümelerin yönetiminde en iyi uygulamalar için bağlantılar sağlar. Üretim ortamınızın güvenilirliği iyileştirmek için bu yöntemleri uygulamanız önerilir. Birini [Service Fabric kümesi şablonları](https://github.com/Azure-Samples/service-fabric-cluster-templates) üretim çözümünüze tasarlamaya başlayabileceğiniz ya da bu yöntemler eklemek için mevcut kullanarak şablonunuzu güncelleştirin.

## <a name="security"></a>Güvenlik

* [En iyi güvenlik uygulamaları](service-fabric-best-practices-security.md)

## <a name="networking"></a>Ağ

* [Ağ için en iyi uygulamalar](service-fabric-best-practices-networking.md)

## <a name="compute-planning-and-scaling"></a>İşlem planlama ve ölçeklendirme

* [İşlem ölçeklendirme için en iyi yöntemler](service-fabric-best-practices-capacity-scaling.md)
* [İşlem kapasitesini planlama](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-capacity)

## <a name="infrastructure-as-code"></a>Kod olarak altyapı

* [Kod olarak altyapı uygulamak için en iyi yöntemler](service-fabric-best-practices-infrastructure-as-code.md)

## <a name="monitoring-and-diagnostics"></a>İzleme ve tanılama

* [Küme izleme ve tanılama için en iyi uygulamalar](service-fabric-best-practices-monitoring.md)

## <a name="application-design"></a>Uygulama tasarımı

* [Uygulama tasarımı için en iyi uygulamalar](service-fabric-best-practices-applications.md)

## <a name="checklist"></a>Denetim listesi

Önceki bölümlerde önerilen yöntemler uyguladıktan sonra üretim hazırlık listesindeki tüm iyi entegre ettik emin olun:
* [Azure Service Fabric üretim hazırlık denetim listesi](https://docs.microsoft.com/azure/service-fabric/service-fabric-production-readiness-checklist)

## <a name="next-steps"></a>Sonraki adımlar

* Vm'leri veya Windows Server çalıştıran bilgisayarlarda bir küme oluşturun: [Windows Server için Service Fabric kümesi oluşturma](service-fabric-cluster-creation-for-windows-server.md)
* Bir küme sanal makineleri veya Linux çalıştıran bilgisayarlara oluşturun: [Bir Linux kümesi oluşturma](service-fabric-cluster-creation-via-portal.md)
* Service Fabric sorunlarını giderme: [Sorun giderme kılavuzları](https://github.com/Azure/Service-Fabric-Troubleshooting-Guides)