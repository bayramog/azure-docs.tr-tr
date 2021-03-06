---
author: vladvino
ms.service: api-management
ms.topic: include
ms.date: 11/09/2018
ms.author: vlvinogr
ms.openlocfilehash: dff01f8bc4a4cf58d1ed503b69a29dadc367fecb
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/13/2019
ms.locfileid: "66248986"
---
## <a name="how-apim-proxy-server-responds-with-ssl-certificates-in-the-tls-handshake"></a>APIM Proxy sunucusu TLS el sıkışma SSL sertifikalarının nasıl yanıt verir

### <a name="clients-calling-with-sni-header"></a>SNI üstbilgiyle çağırma istemcileri
Müşteri proxy'si için yapılandırıldığında bir veya birden fazla özel etki alanı varsa, APIM HTTPS isteklerini özel yönetilenden (örneğin, contoso.com) yanı sıra varsayılan etki alanı yanıtlayan (örneğin, apım-hizmet-name.azure-api.net). Sunucu adı belirtme (SNI) üst bilgisindeki bilgilere dayanarak, APIM, uygun sunucu sertifikası ile yanıt verir.

### <a name="clients-calling-without-sni-header"></a>SNI üst bilgisi olmadan çağırma istemcileri
Müşteri göndermediğinden bir istemci kullanıp kullanmadığını [SNI](https://tools.ietf.org/html/rfc6066#section-3) üst bilgi, APIM şu mantığa göre yanıtları oluşturur:

* Hizmet proxy'si için yapılandırıldığında yalnızca bir özel etki alanı varsa, varsayılan sertifika Proxy özel etki alanı verilmiş olan sertifikadır.
* Hizmet birden fazla özel etki alanları proxy'si için yapılandırıldığında değilse (yalnızca desteklenen **Premium** katman), müşterinin hangi sertifikanın varsayılan sertifika olmalıdır belirleyebilirsiniz. Varsayılan Sertifika ayarlamak için [defaultSslBinding](https://docs.microsoft.com/rest/api/apimanagement/2019-01-01/apimanagementservice/createorupdate#hostnameconfiguration) özelliğinin ayarlanması true ("defaultSslBinding": "true"). Müşteri özelliği ayarlı değil, varsayılan varsayılan ara sunucu etki alanına *.azure-api.net barındırılan sertifikanın sertifikadır.

## <a name="support-for-putpost-request-with-large-payload"></a>Büyük yük ile PUT/POST isteği için destek

APIM Proxy sunucusu, istemci tarafı sertifikalarını HTTPS kullanırken büyük yükü istekle destekler (örneğin, yükü > 40 KB). Sunucunun isteği dondurma gelen önlemek için müşterilerin özelliği ayarlayabilirsiniz ["negotiateClientCertificate": "true"](https://docs.microsoft.com/rest/api/apimanagement/2019-01-01/ApiManagementService/CreateOrUpdate#hostnameconfiguration) üzerinde Proxy konak adı. Özellik ayarlanmışsa true olarak, istemci sertifika herhangi bir HTTP isteği exchange önce SSL/TLS bağlantı zaman istenir. Olduğundan, ayar uygulanır **Proxy konak adı** düzeyi, tüm bağlantı istekleri için istemci sertifikası isteyin. Müşteriler, en fazla 20 özel etki alanları için Proxy yapılandırabilirsiniz (yalnızca desteklenen **Premium** katmanı) ve geçici olarak bu sınırlama.

