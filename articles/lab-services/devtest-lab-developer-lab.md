---
title: Azure DevTest Labs geliştiriciler için kullanın. | Microsoft Docs
description: Geliştirici senaryoları için Azure DevTest Labs'i kullanmayı öğrenin.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 5a293946e4672e7737f912f42511ad0907ba4a81
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/13/2019
ms.locfileid: "61294008"
---
# <a name="use-azure-devtest-labs-for-developers"></a>Azure DevTest Labs geliştiriciler için kullanın.
Azure DevTest Labs, çok sayıda önemli senaryoyu uygulamak için kullanılabilir ancak başlıca senaryolardan biri, geliştiriciler için geliştirme makinelerini barındırmak üzere DevTest Labs kullanmayı içerir. Bu senaryoda DevTest Labs şu avantajları sağlar:

- Geliştiriciler, geliştirme makinelerinde isteğe bağlı olarak hızla sağlayabilirsiniz.
- Geliştiriciler, geliştirme makinelerini gerekli olan her durumda özelleştirebilir.
- Yöneticiler, sağlayarak maliyetleri denetleyebilirsiniz:
  - Geliştiriciler, geliştirme için ihtiyaç duydukları çok daha fazla VM alınamıyor.
  - Vm'leri zaman kullanımda kapatılır. 

![Eğitim için DevTest Labs kullanma](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

Bu makalede, geliştirici gereksinimlerini karşılamak için kullanılabilecek çeşitli Azure DevTest Labs özellikleri ve bir laboratuvarı ayarlama izleyebileceğiniz ayrıntılı adımlar hakkında bilgi edinin.

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a>Azure DevTest Labs ile geliştirme ortamları uygulama
1. **Laboratuvar oluşturma** 
   
    Labs Azure DevTest labs'deki başlangıç noktasıdır. Bir laboratuvar oluşturduktan sonra hızlı bir şekilde oluşturabileceğiniz VM görüntülerini tanımlama, maliyetleri ve daha fazlasını denetlemek için ilkeler ayarlama kullanıcı (geliştiriciler) bir laboratuvara ekleme gibi görevleri gerçekleştirebilir.  
   
    Aşağıdaki tabloda bağlantıları tıklayarak daha fazla bilgi:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure DevTest Labs'de Laboratuvar oluşturma](devtest-lab-create-lab.md) |Azure portalında Azure DevTest Labs'de Laboratuvar oluşturma konusunda bilgi edinin. |
2. **VM hazır Market görüntüleri hem de özel görüntüleri kullanarak dakikalar içinde oluşturun.** 
   
    Azure Market'te çok çeşitli görüntüleri hazır görüntülerini çekme ve Laboratuvardaki ayıklanarak. Kullanıma hazır görüntüler gereksinimlerinizi karşılamıyorsa, bir laboratuvar Azure Market, ihtiyacınız olan tüm yazılım yükleme ve kaydetme VM bir laboratuvara özel görüntü olarak kullanıma hazır bir görüntü kullanarak sanal makine oluşturarak, özel bir görüntü oluşturabilirsiniz.

    Özel görüntüleri kullanarak bir görüntü factory oluşturup görüntülerinizi dağıtmak için kullanmayı düşünün. Bir görüntü fabrikası düzenli olarak oluşturan ve yapılandırılmış görüntülerinizin otomatik olarak dağıtır yapılandırma olarak kodu bir çözümdür. Bu, temel işletim sistemi ile bir VM oluşturulduktan sonra sistemi el ile yapılandırmak için gereken süreyi kaydeder.
  
    Aşağıdaki tabloda bağlantıları tıklayarak daha fazla bilgi:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure Market görüntülerini yapılandırma](devtest-lab-configure-marketplace-images.md) |Beyaz liste Azure Market görüntülerini yalnızca, geliştiriciler için istediğiniz görüntüleri seçim için kullanılabilir hale getirme öğrenin.|
   | [Özel görüntü oluşturma](devtest-lab-create-template.md) |Böylece geliştiriciler özel görüntüyü kullanarak VM'yi hızlı bir şekilde oluşturabilir, ihtiyacınız olan yazılımları önceden yükleyerek özel bir görüntü oluşturun.|
   | [Görüntü factory hakkında bilgi edinin](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |Ayarlama ve görüntü factory'yi açıklayan bir video izleyin.|

3. **Geliştirici makineleri için yeniden kullanılabilir şablonları oluşturma** 
   
    Azure DevTest labs'deki bir formül, bir VM oluşturmak için kullanılan varsayılan özellik değerleri listesidir. Görüntü, bir VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağ'ı seçerek, laboratuvarda bir formül oluşturabilirsiniz. Her geliştirici bir laboratuvar formülü görebilir ve bir VM oluşturmak için bunu kullanın. 
   
    Aşağıdaki tabloda bağlantıları tıklayarak daha fazla bilgi:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Sanal makineler oluşturmak için DevTest Labs formülleri yönetme](devtest-lab-manage-formulas.md) |Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağ seçerek bir formülü nasıl oluşturacağınızı öğrenin.|

4. **Esnek VM özelleştirmeyi etkinleştirmek için yapıtlar oluşturma**

   Yapıtlar, VM sağlandıktan sonra Uygulamanızı yapılandırmak ve dağıtmak için kullanılır. Yapıtlar şunlar olabilir:

   - Aracılar, fiddler'ı ve Visual Studio gibi - VM üzerinde yüklemek istediğiniz araçlar.
   - Bir depoyu kopyalama gibi VM üzerinde-çalıştırmak istediğiniz eylemler.
   - Test etmek istediğiniz uygulamalar.

   Kullanılabilir çıkış,-hazır birçok yapıtları zaten var. Daha fazla özelleştirme belirli ihtiyaçlarınız için isterseniz kendi özel yapıtlar oluşturabilirsiniz.

   Aşağıdaki tabloda bağlantıları tıklayarak daha fazla bilgi:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [DevTest Labs sanal makinenizin özel yapıtlar oluşturma](devtest-lab-artifact-author.md) |Sanal makineler için kendi özel yapıtlar Laboratuvarınızı oluşturun.|
   | [Özel yapıtlar ve Azure Resource Manager şablonlarını kullanmak için Azure DevTest Labs'de depolamak için bir Git deposu ekleme](devtest-lab-add-artifact-repo.md) |Kendi özel Git deposunda özel yapıtlarınızı depolamayı öğrenin.|

5. **Maliyetleri**
   
    Azure DevTest Labs Laboratuvar bir uygulama geliştiricisi tarafından oluşturulan VM'ler en fazla sayısını belirtmek için Laboratuvardaki bir ilke ayarlamanıza olanak tanır. 
   
    Geliştirme takımınıza çalışma kümesi varsa zamanlama ve günün belirli bir zamanda tüm sanal makineleri durdurmak ve ardından bunları sonraki gün otomatik olarak yeniden istiyorsanız, laboratuar ortamında otomatik kapatma ve otomatik başlatma ilkeleri ayarlayarak, kolayca gerçekleştirebilirsiniz. 
   
    Uygulama geliştirme tamamlandığında, son olarak, tüm VM'ler aynı anda tek bir PowerShell betiğini çalıştırarak silebilirsiniz. 
   
    Aşağıdaki tabloda bağlantıları tıklayarak daha fazla bilgi:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Laboratuvar ilkelerini tanımlama](devtest-lab-set-lab-policy.md) |Laboratuvar ilkeleri ayarlayarak maliyetleri denetleyin. |
   | [Tüm Laboratuvar bir PowerShell Betiği kullanarak Vm'leri Sil](devtest-lab-faq.md#how-do-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Tek bir işlemde tüm labs, geliştirme tamamlandıktan sonra silin.|

1. **Bir VM'ye sanal ağ ekleme** 
   
    DevTest Labs, her bir laboratuvar oluşturulduğunda yeni bir sanal ağ (VNET) oluşturur. Kendi sanal ağ – Örneğin, ExpressRoute veya siteden siteye VPN kullanarak – yapılandırdıysanız, böylece VM'ler oluşturulurken kullanılabilir, bu sanal ağ, Laboratuvar sanal ağ ayarları ekleyebilirsiniz.

    Ayrıca, bir Azure Active Directory etki alanı birleşim yapıya VM oluşturulduğunda, bir VM için bir etki alanına katılacak kullanılabilir yoktur. 
   
    Aşağıdaki tabloda bağlantıları tıklayarak daha fazla bilgi:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure DevTest Labs'de sanal ağ yapılandırma](devtest-lab-configure-vnet.md) |Azure portalını kullanarak Azure DevTest Labs sanal ağ yapılandırma konusunda bilgi edinin.|

6. **Her laboratuar paylaşabilir**
   
    Labs, geliştiricilere paylaşan bir bağlantıyı kullanarak doğrudan erişilebilir. Sahip oldukları sürece Yöneticiler bile bir Azure hesabınızın olması gerekmez bir [Microsoft hesabı](devtest-lab-faq.md#what-is-a-microsoft-account). Geliştiriciler, diğer geliştiriciler tarafından oluşturulan sanal makineler göremez.  
   
    Aşağıdaki tabloda bağlantıları tıklayarak daha fazla bilgi:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Bir geliştirici, Azure DevTest labs'deki bir laboratuvara ekleme](devtest-lab-add-devtest-user.md) |Geliştiriciler için Laboratuvarınızı eklemek için Azure portalını kullanın.|
   | [Geliştiriciler bir PowerShell betiğini kullanarak laboratuvara ekleme](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Laboratuvarınız için ekleme geliştiriciler otomatikleştirmek için PowerShell kullanın. |
   | [Laboratuvar için bir bağlantı alma](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Nasıl geliştiriciler bir laboratuvar köprü üzerinden doğrudan erişebilirsiniz öğrenin.|

7. **Diğer takımları için laboratuvar oluşturmayı otomatikleştirme** 
   
    Laboratuvar oluşturma, Resource Manager şablonu oluşturarak ve onu tekrar tekrar aynı Laboratuarları oluşturmak için kullanılarak özel ayarları da dahil olmak üzere otomatik hale getirebilirsiniz. 
   
    Aşağıdaki tabloda bağlantıları tıklayarak daha fazla bilgi:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Resource Manager şablonu kullanarak Laboratuvar oluşturma](devtest-lab-faq.md#how-do-i-create-a-lab-from-a-resource-manager-template) |Resource Manager şablonlarını kullanarak Azure DevTest Labs laboratuvarlar oluşturun. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

