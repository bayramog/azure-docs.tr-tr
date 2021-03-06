---
title: include dosyası
description: include dosyası
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 10/04/2019
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 12c28969ed00a1370b90e06e9d57cd666c50ea29
ms.sourcegitcommit: c22327552d62f88aeaa321189f9b9a631525027c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73524027"
---
1. [Azure Portal](https://portal.azure.com) menüsünde **kaynak oluştur**' u seçin. 

   ![Azure portal bir kaynak oluşturun](./media/vpn-gateway-add-gw-rm-portal-include/azure-portal-create-resource.png)
2. Market 'te **Ara** alanına ' sanal ağ geçidi ' yazın. Arama sonuçlarında **Sanal ağ geçidi** seçeneğini bulun ve girişe tıklayın. **Sanal ağ geçidi** sayfasında **Oluştur**' a tıklayın. Bu işlem **Sanal ağ geçidi oluşturma** sayfasını açar.

   ![Sanal ağ geçidi sayfası alanı oluştur](./media/vpn-gateway-add-gw-rm-portal-include/p2sgw.png "Sanal ağ geçidi sayfası alanı oluştur")

   ![Sanal ağ geçidi sayfası alanı oluştur](./media/vpn-gateway-add-gw-rm-portal-include/p2sgw2.png "Sanal ağ geçidi sayfası alanı oluştur")
3. **Sanal ağ geçidi oluştur** sayfasında, sanal ağ geçidinize ait değerleri girin.

   **Proje ayrıntıları**

   - **Abonelik**: açılan listeden kullanmak istediğiniz aboneliği seçin.
   - **Kaynak grubu**: Bu sayfada Sanal ağınızı seçtiğinizde bu ayar tekrar doldurulur.

   **Örnek ayrıntıları**

   - **Ad**: Ağ geçidinizi adlandırın. Ağ geçidinizi adlandırma ağ geçidi alt ağını adlandırmayla aynı değildir. Bu ad, oluşturduğunuz ağ geçidi nesnesinin adıdır.
   - **Bölge**: Bu kaynağı oluşturmak istediğiniz bölgeyi seçin. Ağ geçidinin bölgesi, sanal ağ ile aynı olmalıdır.
   - **Ağ geçidi türü**: **VPN**’i seçin. VPN ağ geçitleri, **VPN** sanal ağ geçidi türünü kullanır. 
   - **VPN türü**: Yapılandırmanızla ilgili belirtilen VPN türünü seçin. Çoğu yapılandırma, Yol Tabanlı bir VPN türü gerektirir.
   - **SKU**: Açılır listeden ağ geçidi SKU’sunu seçin. Açılır listede sıralanan SKU’lar seçtiğiniz VPN türüne bağlıdır. Ağ geçidi SKU’ları hakkında bilgi için bkz. [Ağ geçidi SKU’ları](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).

      **Sanal ağ**: Bu ağ geçidini eklemek istediğiniz sanal ağı seçin.

      **Ağ geçidi alt ağ adres aralığı**: Bu alan yalnızca VNET 'iniz bir ağ geçidi alt ağına sahip değilse görüntülenir. Mümkünse, aralığı/27 veya daha büyük (/26,/25 vb.) aralığı yapın. /28 ' den küçük bir Aralık oluşturmanız önerilmez. Zaten bir ağ geçidi alt ağınız varsa, sanal ağınıza giderek GatewaySubnet ayrıntılarını görüntüleyebilirsiniz. Aralığı görüntülemek için **alt ağlar** ' a tıklayın. Aralığı değiştirmek istiyorsanız, GatewaySubnet 'i silip yeniden oluşturabilirsiniz.

   **Genel IP adresi**: Bu ayar, VPN ağ geçidiyle ilişkilendirilen genel IP adresi nesnesini belirtir. VPN ağ geçidi oluşturulduğunda genel IP adresi bu nesneye dinamik olarak atanır. Genel IP adresi, yalnızca ağ geçidi silinip yeniden oluşturulduğunda değişir. VPN ağ geçidiniz üzerinde gerçekleştirilen yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında değişmez.

     - **Genel IP adresi**: **Yeni oluştur** seçili kalsın.
     - **Genel IP adresi adı**: metin kutusuna, genel IP adresi örneğiniz için bir ad yazın.
     - **Atama**: VPN Gateway yalnızca dinamik destekler.

   **Etkin-etkin mod**: yalnızca etkin-etkin ağ geçidi yapılandırması oluşturuyorsanız **etkin-etkin modunu etkinleştir** ' i seçin. Aksi takdirde bu ayarı seçmeyin.

   Yapılandırmanız için **BGP ASN yapılandır** ayarı özellikle gerekli değilse bu ayarı işaretlemeyin. Bu ayar gerekliyse varsayılan ASN değeri 65515’tir ancak bu değiştirilebilir.

4. Doğrulamayı çalıştırmak için **gözden geçir + oluştur** ' a tıklayın. Doğrulama başarılı olduktan sonra, VPN ağ geçidini dağıtmak için **Oluştur** ' a tıklayın. Bir ağ geçidinin, tam olarak oluşturulması ve dağıtılması 45 dakika sürebilir. Dağıtım durumunu ağ geçidinizin Genel Bakış sayfasında görebilirsiniz.

Ağ geçidi oluşturulduktan sonra, portalda sanal ağa bakarak bu ağ geçidine atanmış IP adresini görüntüleyebilirsiniz. Ağ geçidi bağlı bir cihaz gibi görüntülenir.
