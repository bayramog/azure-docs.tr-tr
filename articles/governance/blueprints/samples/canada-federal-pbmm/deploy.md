---
title: Kanada Federal pbmm şema örnek-dağıtım adımları
description: Şema yapıt parametresi ayrıntıları dahil olmak üzere Kanada Federal pbmm şema örneği için adımları dağıtın.
ms.date: 09/05/2019
ms.topic: conceptual
ms.openlocfilehash: 788c52ee9a2bf9a0a2c506c2a34d221ff08bd0af
ms.sourcegitcommit: 49cf9786d3134517727ff1e656c4d8531bbbd332
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74038409"
---
# <a name="deploy-the-canada-federal-pbmm-blueprint-samples"></a>Kanada Federal pbmm şema örneklerini dağıtma

Kanada Federal pbmm şema örneklerini dağıtmak için aşağıdaki adımlar gerçekleştirilmelidir:

> [!div class="checklist"]
> - Örnekten yeni bir şema oluştur
> - Örnek kopyanızı **yayımlandı** olarak işaretleyin
> - Şema kopyanızı mevcut bir aboneliğe atama

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free) oluşturun.

## <a name="create-blueprint-from-sample"></a>Örnekten şema oluştur

İlk olarak, bir başlangıç olarak örneği kullanarak ortamınızda yeni bir şema oluşturarak şema örneğini uygulayın.

1. **Tüm hizmetler** ' i seçin ve sol bölmedeki **ilke** ara ' yı seçin. **İlke** sayfasında, **planlar**' ı seçin.

1. Soldaki **Başlarken** sayfasında, şema _Oluştur_altında **Oluştur** düğmesini seçin.

1. _Diğer örnekler_ altında **Kanada Federal pbmm** şema örneğini bulun ve **Bu örneği kullan**' ı seçin.

1. Şema örneği _hakkında temel bilgileri_ girin:

   - **Şema adı**: şema örneğinin kopyasına bir ad verin.
   - **Tanım konumu**: üç noktayı kullanın ve örneğin kopyasını kaydetmek için yönetim grubunu seçin.

1. Sayfanın üst kısmındaki _yapıtlar_ sekmesini veya sonraki: sayfanın en altındaki **yapıtları** seçin.

1. Şema örneğini oluşturan yapıtların listesini gözden geçirin. Yapıtların çoğunda, daha sonra tanımlayacağımız parametreler vardır. Şema örneğini gözden geçirmeyi bitirdiğinizde **Taslağı kaydet** ' i seçin.

## <a name="publish-the-sample-copy"></a>Örnek kopyayı Yayımla

Şema örneğinin kopyası artık ortamınızda oluşturulmuştur. **Taslak** modunda oluşturulur ve atanmadan ve dağıtılmadan önce **yayımlanmaları** gerekir. Şema örneğinin kopyası ortamınıza ve gereksinimlerinize göre özelleştirilebilir, ancak bu değişiklik bu değişikliği standart dışında taşıyabilir.

1. **Tüm hizmetler** ' i seçin ve sol bölmedeki **ilke** ara ' yı seçin. **İlke** sayfasında, **planlar**' ı seçin.

1. Sol taraftaki **Blueprint tanımları** sayfasını seçin. Şemayı kullanarak şema örneğinin kopyasını bulun ve ardından seçin.

1. Sayfanın üst kısmındaki şemayı **Yayımla** ' yı seçin. Sağ taraftaki yeni sayfada, şema örneğinin kopyası için bir **Sürüm** belirtin. Daha sonra bir değişiklik yaparsanız, bu özellik için faydalıdır. "Kanada Federal pbmm şema örneğinden yayımlanan ilk sürüm" gibi **değişiklik notları** sağlayın. Ardından sayfanın alt kısmında **Yayımla** ' yı seçin.

## <a name="assign-the-sample-copy"></a>Örnek kopyayı atama

Şema örneğinin kopyası başarıyla **yayımlandıktan**sonra, kaydedildiği yönetim grubu içindeki bir aboneliğe atanabilir. Bu adım, her bir şema örneğinin kopyasının her dağıtımını yapmak için parametrelerin sağlandığı yerdir.

1. **Tüm hizmetler** ' i seçin ve sol bölmedeki **ilke** ara ' yı seçin. **İlke** sayfasında, **planlar**' ı seçin.

1. Sol taraftaki **Blueprint tanımları** sayfasını seçin. Şemayı kullanarak şema örneğinin kopyasını bulun ve ardından seçin.

1. Şema tanım sayfasının en üstünde şema **ata** ' yı seçin.

1. Şema atamasının parametre değerlerini sağlayın:

   - Temel Bilgiler

     - **Abonelikler**: şema örneğinin kopyasını kaydettiğiniz yönetim grubundaki bir veya daha fazla abonelik seçin. Birden fazla abonelik seçerseniz, girilen parametreleri kullanarak her biri için bir atama oluşturulur.
     - **Atama adı**: ad, BLUEPRINT adına göre önceden doldurulur.
       Gerektiğinde değiştirin veya olduğu gibi bırakın.
     - **Konum**: yönetilen kimliğin oluşturulacağı bölgeyi seçin. Azure Blueprint bu yönetilen kimliği kullanarak tüm yapıtları atanmış şemaya dağıtır. Daha fazla bilgi için bkz. [Azure kaynakları için yönetilen kimlikler](../../../../active-directory/managed-identities-azure-resources/overview.md).
     - Şema **tanımı sürümü**: şema örneğinin kopyasının **yayınlanmış** bir sürümünü seçin.

   - Kilit ataması

     Ortamınız için BLUEPRINT Lock ayarını seçin. Daha fazla bilgi için bkz. [şema kaynağı kilitleme](../../concepts/resource-locking.md).

   - Yönetilen Kimlik

     Varsayılan sistem tarafından _atanmış_ yönetilen kimlik seçeneğini bırakın.

   - Yapıt parametreleri

     Bu bölümde tanımlanan parametreler, tanımlanan yapıt için geçerlidir. Bu parametreler, Blueprint atama sırasında tanımlandıklarından [dinamik parametrelerdir](../../concepts/parameters.md#dynamic-parameters) . Tam liste veya yapıt parametreleri ve açıklamaları için bkz. [yapıt parametreleri tablosu](#artifact-parameters-table).

1. Tüm parametreler girildikten sonra sayfanın alt kısmındaki **ata** ' yı seçin. Şema ataması oluşturulur ve yapıt dağıtımı başlar. Dağıtım kabaca bir saat sürer. Dağıtımın durumunu denetlemek için, BLUEPRINT atamasını açın.

> [!WARNING]
> Azure şemaları hizmeti ve yerleşik şema örnekleri **ücretsiz olarak ücretsizdir**. Azure kaynakları [ürüne göre fiyatlandırılır](https://azure.microsoft.com/pricing/). Bu şema örneği tarafından dağıtılan çalışan kaynakların maliyetini tahmin etmek için [fiyatlandırma hesaplayıcısını](https://azure.microsoft.com/pricing/calculator/) kullanın.

## <a name="artifact-parameters-table"></a>Yapıt parametreleri tablosu

Aşağıdaki tabloda, şema yapıt parametrelerinin bir listesi verilmiştir:

Yapıt adı|Yapıt türü|Parametre adı|Açıklama|
|-|-|-|-|
|\[Önizleme\]: Linux sanal makineleri için Log Analytics aracısını dağıtmayı |İlke ataması |Linux VM 'Ler için Log Analytics çalışma alanı |Daha fazla bilgi için [Azure portal Log Analytics çalışma alanı oluşturma](../../../../azure-monitor/learn/quick-create-workspace.md)bölümüne bakın. |
|\[Önizleme\]: Linux sanal makineleri için Log Analytics aracısını dağıtmayı |İlke ataması |İsteğe bağlı: kapsama eklemek için desteklenen Linux işletim sistemini destekleyen VM görüntülerinin listesi |Boş bir dizi, isteğe bağlı parametre olmadığını göstermek için kullanılabilir: `[]` |
|\[Önizleme\]: Windows Vm'leri için Log Analytics aracısını dağıtmayı |İlke ataması |İsteğe bağlı: kapsama eklemek için desteklenen Windows işletim sistemini destekleyen VM görüntülerinin listesi |Boş bir dizi, isteğe bağlı parametre olmadığını göstermek için kullanılabilir: `[]` |
|\[Önizleme\]: Windows Vm'leri için Log Analytics aracısını dağıtmayı |İlke ataması |Windows VM 'Leri için Log Analytics çalışma alanı |Daha fazla bilgi için [Azure portal Log Analytics çalışma alanı oluşturma](../../../../azure-monitor/learn/quick-create-workspace.md)bölümüne bakın. |
|\[önizleme\]: denetim gereksinimlerini desteklemek için Kanada Federal PBMM denetimlerini denetleme ve belirli VM uzantılarını dağıtma |İlke ataması |VM 'Lerin yapılandırılması gereken Log Analytics çalışma alanı KIMLIĞI |Bu, VM 'Lerin için yapılandırılması gereken Log Analytics çalışma alanının KIMLIĞIDIR (GUID). |
|\[önizleme\]: denetim gereksinimlerini desteklemek için Kanada Federal PBMM denetimlerini denetleme ve belirli VM uzantılarını dağıtma |İlke ataması |Tanılama günlükleri etkinleştirilmiş olması gereken kaynak türlerinin listesi |Tanılama günlüğü ayarı etkinleştirilmemişse denetlenecek kaynak türleri listesi. Kabul edilebilir değerler, [Azure izleyici tanılama günlükleri şemalarında](../../../../azure-monitor/platform/diagnostic-logs-schema.md#supported-log-categories-per-resource-type)bulunabilir. |
|\[önizleme\]: denetim gereksinimlerini desteklemek için Kanada Federal PBMM denetimlerini denetleme ve belirli VM uzantılarını dağıtma |İlke ataması |Yöneticiler grubu |Grubu. Örnek: `Administrator; myUser1; myUser2` |
|\[önizleme\]: denetim gereksinimlerini desteklemek için Kanada Federal PBMM denetimlerini denetleme ve belirli VM uzantılarını dağıtma |İlke ataması |Windows VM yöneticileri grubuna dahil edilecek kullanıcıların listesi |Yöneticiler yerel grubuna dahil edilecek üyelerin noktalı virgülle ayrılmış listesi. Örnek: `Administrator; myUser1; myUser2` |
|Depolama hesaplarında Gelişmiş tehdit koruması dağıtma |İlke ataması |Etki |İlke etkileri hakkında daha fazla bilgi için bkz. [Azure Ilke efektlerini anlama](../../../policy/concepts/effects.md). |
|SQL Server 'lar üzerinde denetim dağıtma |İlke ataması |Bekletme döneminin gün cinsinden değer (0 sınırsız saklama anlamına gelir) |Bekletme günleri (belirtilmemişse, _180_ gün) |
|SQL Server 'lar üzerinde denetim dağıtma |İlke ataması |SQL Server denetimi için depolama hesabının kaynak grubu adı |Denetim, veritabanı olaylarını Azure Depolama hesabınızdaki bir denetim günlüğüne yazar (bir depolama hesabı, bu bölgedeki tüm sunucular tarafından paylaşılan bir SQL Server oluşturulduğu her bölgede oluşturulur). Önemli-denetimin düzgün çalışması için kaynak grubunu veya depolama hesaplarını silmeyin veya yeniden adlandırmayın. |
|Ağ güvenlik grupları için tanılama ayarlarını dağıtma |İlke ataması |Ağ güvenlik grubu Tanılama için depolama hesabı öneki |Bu ön ek, oluşturulan depolama hesabı adını biçimlendirmek için ağ güvenlik grubu konumuyla birleştirilir. |
|Ağ güvenlik grupları için tanılama ayarlarını dağıtma |İlke ataması |Ağ güvenlik grubu Tanılama için depolama hesabının kaynak grubu adı (var olmalıdır) |Depolama hesabının oluşturulduğu kaynak grubu. Bu kaynak grubu zaten var olmalıdır. |

## <a name="next-steps"></a>Sonraki adımlar

Kanada Federal PBMM örneğini dağıtma adımlarını gözden geçirdiğinize göre, genel bakış ve denetim eşlemesi hakkında bilgi edinmek için aşağıdaki makaleleri ziyaret edin:

> [!div class="nextstepaction"]
> [Kanada Federal PBMM şemaları-genel bakış](./index.md)
> [Kanada Federal Pbmm şemaları-denetim eşleme](./control-mapping.md)

Şemalar ve bunların kullanımı hakkındaki diğer makaleler:

- [Şema yaşam döngüsü](../../concepts/lifecycle.md) hakkında bilgi edinin.
- [Statik ve dinamik parametrelerin](../../concepts/parameters.md) kullanımını anlayın.
- [Şema sıralama düzenini](../../concepts/sequencing-order.md) özelleştirmeyi öğrenin.
- [Şema kaynak kilitleme](../../concepts/resource-locking.md) özelliğini kullanmayı öğrenin.
- [Mevcut atamaları güncelleştirmeyi](../../how-to/update-existing-assignments.md) öğrenin.