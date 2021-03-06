---
title: Web API 'Lerini çağıran Daemon uygulaması (uygulama yapılandırma)-Microsoft Identity platform
description: Web API 'Lerini (App Configuration) çağıran bir Daemon uygulaması derlemeyi öğrenin
services: active-directory
documentationcenter: dev-center-name
author: jmprieur
manager: CelesteDG
editor: ''
ms.service: active-directory
ms.subservice: develop
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 10/30/2019
ms.author: jmprieur
ms.custom: aaddev
ms.collection: M365-identity-device-management
ms.openlocfilehash: 32fbd4af78e02dad2a8a74ee21f9cb8c6ef0a976
ms.sourcegitcommit: 98ce5583e376943aaa9773bf8efe0b324a55e58c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73175500"
---
# <a name="daemon-app-that-calls-web-apis---code-configuration"></a>Web API 'Lerini çağıran Daemon uygulaması-kod yapılandırması

Web API 'Lerini çağıran Daemon uygulamanız için kodu yapılandırmayı öğrenin.

## <a name="msal-libraries-supporting-daemon-apps"></a>Daemon uygulamalarını destekleyen MSAL kitaplıkları

Daemon uygulamalarını destekleyen Microsoft kitaplıkları şunlardır:

  MSAL kitaplığı | Açıklama
  ------------ | ----------
  ![MSAL.NET](media/sample-v2-code/logo_NET.png) <br/> MSAL.NET  | Bir Daemon uygulaması derlemek için desteklenen platformlar .NET Framework ve .NET Core platformları (UWP, Xamarin. iOS ve Xamarin. Android değil, ortak istemci uygulamaları oluşturmak için kullanılır)
  ![Python](media/sample-v2-code/logo_python.png) <br/> MSAL Python | Geliştirme devam ediyor-genel önizlemede
  ![Java](media/sample-v2-code/logo_java.png) <br/> MSAL Java | Geliştirme devam ediyor-genel önizlemede

## <a name="configuration-of-the-authority"></a>Yetkilisinin yapılandırması

Daemon uygulamalarının temsilci izinleri kullanmadığında, ancak uygulama izinleri, *Desteklenen hesap türü* *herhangi bir kurumsal dizin ve kişisel Microsoft hesabında hesap olamaz (örneğin, Skype, Xbox, Outlook.com)* . Aslında, Microsoft kişisel hesapları için Daemon uygulamasına izin vermek üzere kiracı yöneticisi yoktur. *Kuruluşumdaki hesaplar* veya *herhangi bir kuruluştaki hesaplar*' ı seçmeniz gerekir.

Bu nedenle, uygulama yapılandırmasında belirtilen yetkilinin kiracı ile bağlantılı olması gerekir (kiracı KIMLIĞI veya kuruluşunuzla ilişkili bir etki alanı adı belirterek).

Bir ISV iseniz ve çok kiracılı bir araç sağlamak istiyorsanız `organizations` kullanabilirsiniz. Ancak, müşterilere yönetici onayı verme hakkında da dikkat etmeniz gerektiğini unutmayın. Ayrıntılar için [bir kiracının tamamına Izin isteme](v2-permissions-and-consent.md#requesting-consent-for-an-entire-tenant) konusuna bakın. MSAL ' de şu anda bir sınırlama vardır: `organizations` yalnızca istemci kimlik bilgileri bir uygulama gizli anahtarı (sertifika değil) olduğunda izin verilir.

## <a name="application-configuration-and-instantiation"></a>Uygulama yapılandırma ve örnekleme

MSAL kitaplıklarında, istemci kimlik bilgileri (gizli veya sertifika) gizli istemci uygulaması oluşturma parametresi olarak geçirilir.

> [!IMPORTANT]
> Uygulamanız hizmet olarak çalışan bir konsol uygulaması olsa da, bir Daemon uygulaması ise gizli bir istemci uygulaması olması gerekir.

### <a name="configuration-file"></a>Yapılandırma dosyası

Yapılandırma dosyası şunları tanımlar:

- yetkili veya bulut örneği ile Tenantıd
- Uygulama kaydından aldığınız ClientID
- bir istemci parolası ya da bir sertifika

# <a name="nettabdotnet"></a>[.NET](#tab/dotnet)

[.NET Core konsol Daemon](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2) örneğinden [appSettings. JSON](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/blob/master/1-Call-MSGraph/daemon-console/appsettings.json) .

```JSon
{
  "Instance": "https://login.microsoftonline.com/{0}",
  "Tenant": "[Enter here the tenantID or domain name for your Azure AD tenant]",
  "ClientId": "[Enter here the ClientId for your application]",
  "ClientSecret": "[Enter here a client secret for your application]",
  "CertificateName": "[Or instead of client secret: Enter here the name of a certificate (from the user cert store) as registered with your application]"
}
```

Bir clientSecret veya certificateName sağlarsınız. Her iki ayar de dışlamalı.

# <a name="pythontabpython"></a>[Python](#tab/python)

İstemci gizli dizileri ile gizli bir istemci oluştururken, [Python Daemon](https://github.com/Azure-Samples/ms-identity-python-daemon) örneğindeki [Parameters. JSON](https://github.com/Azure-Samples/ms-identity-python-daemon/blob/master/1-Call-MsGraph-WithSecret/parameters.json) yapılandırma dosyası aşağıdaki gibidir.

```Json
{
  "authority": "https://login.microsoftonline.com/Enter_the_Tenant_Name_Here",
  "client_id": "your_client_id",
  "scope": [ "https://graph.microsoft.com/.default" ],
  "secret": "The secret generated by AAD during your confidential app registration",
  "endpoint": "https://graph.microsoft.com/v1.0/users"
}
```

Sertifikalarla gizli bir istemci oluştururken, [Python Daemon](https://github.com/Azure-Samples/ms-identity-python-daemon) örneğindeki [Parameters. JSON](https://github.com/Azure-Samples/ms-identity-python-daemon/blob/master/2-Call-MsGraph-WithCertificate/parameters.json) yapılandırma dosyası aşağıdaki gibidir.

```Json
{
  "authority": "https://login.microsoftonline.com/Enter_the_Tenant_Name_Here",
  "client_id": "your_client_id",
  "scope": [ "https://graph.microsoft.com/.default" ],
  "thumbprint": "790E... The thumbprint generated by AAD when you upload your public cert",
  "private_key_file": "server.pem",
  "endpoint": "https://graph.microsoft.com/v1.0/users"
}
```

# <a name="javatabjava"></a>[Java](#tab/java)

Örnekleri yapılandırmak için MSAL Java dev örneklerinde kullanılan sınıf şunlardır: [TestData](https://github.com/AzureAD/microsoft-authentication-library-for-java/blob/dev/src/samples/public-client/TestData.java).

```Java
public class TestData {

    final static String TENANT_SPECIFIC_AUTHORITY = "https://login.microsoftonline.com/<TenantId>/";
    final static String GRAPH_DEFAULT_SCOPE = "https://graph.microsoft.com/.default";
    final static String CONFIDENTIAL_CLIENT_ID = "";
    final static String CONFIDENTIAL_CLIENT_SECRET = "";
}
```

---

### <a name="instantiation-of-the-msal-application"></a>MSAL uygulamasının örneklemesi

MSAL uygulamasının örneğini oluşturmak için şunları yapmanız gerekir:

- MSAL paketini ekleme, başvuru veya içeri aktarma (dile bağlı olarak)
- Daha sonra, istemci gizli dizileri veya sertifikaları (veya gelişmiş bir senaryo olarak imzalanmış onaylar olarak) kullanıyorsanız, oluşturma işlemi farklı olur

#### <a name="reference-the-package"></a>Pakete başvur

Uygulama kodunuzda MSAL paketine başvurun.

# <a name="nettabdotnet"></a>[.NET](#tab/dotnet)

Uygulamanıza [Microsoft. ıdentityclient](https://www.nuget.org/packages/Microsoft.Identity.Client) NuGet paketini ekleyin.
MSAL.NET ' de, gizli istemci uygulaması `IConfidentialClientApplication` arabirimi tarafından temsil edilir.
Kaynak kodunda MSAL.NET ad alanını kullan

```CSharp
using Microsoft.Identity.Client;
IConfidentialClientApplication app;
```

# <a name="pythontabpython"></a>[Python](#tab/python)

```python
import msal
```

# <a name="javatabjava"></a>[Java](#tab/java)

```java
import com.microsoft.aad.msal4j.ClientCredentialFactory;
import com.microsoft.aad.msal4j.ClientCredentialParameters;
import com.microsoft.aad.msal4j.ConfidentialClientApplication;
import com.microsoft.aad.msal4j.IAuthenticationResult;
```

---

#### <a name="instantiate-the-confidential-client-application-with-client-secrets"></a>Gizli istemci uygulamasının istemci gizli dizileri ile örneğini oluşturma

Gizli istemci uygulamasını bir istemci gizli anahtarı ile örneklendirilecek kod aşağıda verilmiştir:

# <a name="nettabdotnet"></a>[.NET](#tab/dotnet)

```CSharp
app = ConfidentialClientApplicationBuilder.Create(config.ClientId)
           .WithClientSecret(config.ClientSecret)
           .WithAuthority(new Uri(config.Authority))
           .Build();
```

# <a name="pythontabpython"></a>[Python](#tab/python)

```Python
config = json.load(open(sys.argv[1]))

# Create a preferably long-lived app instance which maintains a token cache.
app = msal.ConfidentialClientApplication(
    config["client_id"], authority=config["authority"],
    client_credential=config["secret"],
    # token_cache=...  # Default cache is in memory only.
                       # You can learn how to use SerializableTokenCache from
                       # https://msal-python.rtfd.io/en/latest/#msal.SerializableTokenCache
    )
```

# <a name="javatabjava"></a>[Java](#tab/java)

```Java
ConfidentialClientApplication app = ConfidentialClientApplication.builder(
        TestData.CONFIDENTIAL_CLIENT_ID,
        ClientCredentialFactory.create(TestData.CONFIDENTIAL_CLIENT_SECRET))
        .authority(TestData.TENANT_SPECIFIC_AUTHORITY)
        .build();
```

---

#### <a name="instantiate-the-confidential-client-application-with-client-certificate"></a>İstemci sertifikası Ile gizli istemci uygulaması örneğini oluşturma

Sertifika ile bir uygulama oluşturmak için kod aşağıda verilmiştir:

# <a name="nettabdotnet"></a>[.NET](#tab/dotnet)

```CSharp
X509Certificate2 certificate = ReadCertificate(config.CertificateName);
app = ConfidentialClientApplicationBuilder.Create(config.ClientId)
    .WithCertificate(certificate)
    .WithAuthority(new Uri(config.Authority))
    .Build();
```

# <a name="pythontabpython"></a>[Python](#tab/python)

```Python
config = json.load(open(sys.argv[1]))

# Create a preferably long-lived app instance which maintains a token cache.
app = msal.ConfidentialClientApplication(
    config["client_id"], authority=config["authority"],
    client_credential={"thumbprint": config["thumbprint"], "private_key": open(config['private_key_file']).read()},
    # token_cache=...  # Default cache is in memory only.
                       # You can learn how to use SerializableTokenCache from
                       # https://msal-python.rtfd.io/en/latest/#msal.SerializableTokenCache
    )
```

# <a name="javatabjava"></a>[Java](#tab/java)

MSAL içinde. Java, sertifikalarla gizli istemci uygulaması örneğini oluşturmak için iki oluşturuculara sahiptir:

```Java

InputStream pkcs12Certificate = ... ; /* containing PCKS12 formatted certificate*/
string certificatePassword = ... ;    /* contains the password to access the certificate */

ConfidentialClientApplication app = ConfidentialClientApplication.builder(
        TestData.CONFIDENTIAL_CLIENT_ID,
        ClientCredentialFactory.create(pkcs12Certificate, certificatePassword))
        .authority(TestData.TENANT_SPECIFIC_AUTHORITY)
        .build();
```

or

```Java
PrivateKey key = getPrivateKey(); /* RSA private key to sign the assertion */
X509Certificate publicCertificate = getPublicCertificate(); /* x509 public certificate used as a thumbprint */

ConfidentialClientApplication app = ConfidentialClientApplication.builder(
        TestData.CONFIDENTIAL_CLIENT_ID,
        ClientCredentialFactory.create(rsaPrivateKey, publicKeyCertificate))
        .authority(TestData.TENANT_SPECIFIC_AUTHORITY)
        .build();
```

---

#### <a name="advanced-scenario---instantiate-the-confidential-client-application-with-client-assertions"></a>Gelişmiş senaryo-istemci onaylamaları ile gizli istemci uygulaması örneğini oluşturma

# <a name="nettabdotnet"></a>[.NET](#tab/dotnet)

Gizli istemci uygulaması, bir istemci parolası veya bir sertifika yerine istemci onayları kullanarak kimliğini kanıtlayabilirler.

MSAL.NET, gizli istemci uygulamasına imzalı onaylar sağlamak için iki yönteme sahiptir:

- `.WithClientAssertion()`
- `.WithClientClaims()`

`WithClientAssertion`kullandığınızda, imzalı bir JWT sağlamanız gerekir. Bu gelişmiş senaryo [istemci onaylamaları](msal-net-client-assertions.md) hakkında ayrıntılı

```CSharp
string signedClientAssertion = ComputeAssertion();
app = ConfidentialClientApplicationBuilder.Create(config.ClientId)
                                          .WithClientAssertion(signedClientAssertion)
                                          .Build();
```

`WithClientClaims`kullandığınızda, MSAL.NET, Azure AD ile beklenen talepleri ve göndermek istediğiniz ek istemci taleplerini içeren imzalı bir onaylama işlemi için işlem görür.
Bunun nasıl yapılacağını gösteren bir kod parçacığı aşağıda verilmiştir:

```CSharp
string ipAddress = "192.168.1.2";
var claims = new Dictionary<string, string> { { "client_ip", ipAddress } };
X509Certificate2 certificate = ReadCertificate(config.CertificateName);
app = ConfidentialClientApplicationBuilder.Create(config.ClientId)
                                          .WithAuthority(new Uri(config.Authority))
                                          .WithClientClaims(certificate, claims)
                                          .Build();```
```

Daha ayrıntılı bilgi için bkz. [istemci onayları](msal-net-client-assertions.md).

# <a name="pythontabpython"></a>[Python](#tab/python)

MSAL Python 'da, bu `ConfidentialClientApplication` özel anahtarıyla imzalanacak talepleri kullanarak istemci talepleri sağlayabilirsiniz.

```Python
config = json.load(open(sys.argv[1]))

# Create a preferably long-lived app instance which maintains a token cache.
app = msal.ConfidentialClientApplication(
    config["client_id"], authority=config["authority"],
    client_credential={"thumbprint": config["thumbprint"], "private_key": open(config['private_key_file']).read()},
    client_claims = {"client_ip": "x.x.x.x"}
    # token_cache=...  # Default cache is in memory only.
                       # You can learn how to use SerializableTokenCache from
                       # https://msal-python.rtfd.io/en/latest/#msal.SerializableTokenCache
    )
```

Ayrıntılar için bkz. MSAL Python 'un başvuru belgeleri [ConfidentialClientApplication](https://msal-python.readthedocs.io/en/latest/#msal.ClientApplication.__init__).

# <a name="javatabjava"></a>[Java](#tab/java)

MSAL Java, genel önizlemede. İmzalı Onaylamalar henüz desteklenmiyor.

---

## <a name="next-steps"></a>Sonraki adımlar

# <a name="nettabdotnet"></a>[.NET](#tab/dotnet)

> [!div class="nextstepaction"]
> [Daemon uygulaması-uygulama belirteçleri alınıyor](https://docs.microsoft.com/azure/active-directory/develop/scenario-daemon-acquire-token?tabs=dotnet)

# <a name="pythontabpython"></a>[Python](#tab/python)

> [!div class="nextstepaction"]
> [Daemon uygulaması-uygulama belirteçleri alınıyor](https://docs.microsoft.com/azure/active-directory/develop/scenario-daemon-acquire-token?tabs=python)

# <a name="javatabjava"></a>[Java](#tab/java)

> [!div class="nextstepaction"]
> [Daemon uygulaması-uygulama belirteçleri alınıyor](https://docs.microsoft.com/azure/active-directory/develop/scenario-daemon-acquire-token?tabs=java)

---
