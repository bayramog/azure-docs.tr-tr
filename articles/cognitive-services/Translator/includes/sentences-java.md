---
author: erhopf
ms.service: cognitive-services
ms.topic: include
ms.date: 08/06/2019
ms.author: erhopf
ms.openlocfilehash: 8a567dbbd8c5e752b8d9294623a5f4d3f37e5a05
ms.sourcegitcommit: beb34addde46583b6d30c2872478872552af30a1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69906851"
---
[!INCLUDE [Prerequisites](prerequisites-java.md)]

[!INCLUDE [Set up and use environment variables](setup-env-variables.md)]

## <a name="initialize-a-project-with-gradle"></a>Gradle ile proje başlatma

Bu proje için çalışma dizini oluşturarak başlayalım. Komut satırından (veya terminalden) şu komutu çalıştırın:

```console
mkdir length-sentence-sample
cd length-sentence-sample
```

Sonra, bir Gradle projesi başlatacağız. Bu komut, uygulamanızı oluşturmak ve yapılandırmak için çalışma zamanında kullanılan, en önemlisi `build.gradle.kts`, Gradle için önemli derleme dosyaları oluşturur. Çalışma dizininizden bu komutu çalıştırın:

```console
gradle init --type basic
```

Bir **DSL**seçmeniz Istendiğinde, **Kotlin**' ı seçin.

## <a name="configure-the-build-file"></a>Yapı dosyasını yapılandırma

En `build.gradle.kts` sevdiğiniz IDE veya metin düzenleyicinizle bulun ve açın. Sonra bu derleme yapılandırmasında Kopyala:

```
plugins {
    java
    application
}
application {
    mainClassName = "BreakSentence"
}
repositories {
    mavenCentral()
}
dependencies {
    compile("com.squareup.okhttp:okhttp:2.5.0")
    compile("com.google.code.gson:gson:2.8.5")
}
```

Bu örnekte HTTP istekleri için OkHttp üzerinde bağımlılıklar ve JSON 'u işlemek ve ayrıştırmak için Gson 'un bağımlılıkları olduğuna göz atın. Derleme yapılandırmaları hakkında daha fazla bilgi edinmek istiyorsanız, bkz. [Yeni Gradle derlemeleri oluşturma](https://guides.gradle.org/creating-new-gradle-builds/).

## <a name="create-a-java-file"></a>Bir Java dosyası oluşturma

Örnek uygulamanız için bir klasör oluşturalım. Çalışma dizininizden şunu çalıştırın:

```console
mkdir -p src/main/java
```

Ardından, bu klasörde adlı `BreakSentence.java`bir dosya oluşturun.

## <a name="import-required-libraries"></a>Gerekli kitaplıkları içeri aktar

Bu `BreakSentence.java` içeri aktarma deyimlerini açın ve ekleyin:

```java
import java.io.*;
import java.net.*;
import java.util.*;
import com.google.gson.*;
import com.squareup.okhttp.*;
```


## <a name="define-variables"></a>Değişkenleri tanımlama

İlk olarak, projeniz için bir ortak sınıf oluşturmanız gerekir:

```java
public class BreakSentence {
  // All project code goes here...
}
```

`BreakSentence` Sınıfa bu satırları ekleyin. İlk olarak, abonelik anahtarı ve uç nokta ortam değişkenlerinden okunmakta. Ardından, ile `api-version`birlikte, giriş dilini tanımlayacağınızı fark edeceksiniz. Bu örnekte, Ingilizce olur.

```java
private static String subscriptionKey = System.getenv("TRANSLATOR_TEXT_SUBSCRIPTION_KEY");
private static String endpoint = System.getenv("TRANSLATOR_TEXT_ENDPOINT");
String url = endpoint + "/breaksentence?api-version=3.0&language=en";
```
Bilişsel hizmetler çoklu hizmet aboneliği kullanıyorsanız, istek parametrelerinize de dahil `Ocp-Apim-Subscription-Region` etmeniz gerekir. [Multi-Service aboneliğiyle kimlik doğrulama hakkında daha fazla bilgi edinin](https://docs.microsoft.com/azure/cognitive-services/translator/reference/v3-0-reference#authentication).

## <a name="create-a-client-and-build-a-request"></a>İstemci oluşturma ve istek oluşturma

Örneği oluşturmak için bu satırı `BreakSentence` sınıfa ekleyin: `OkHttpClient`

```java
// Instantiates the OkHttpClient.
OkHttpClient client = new OkHttpClient();
```

Sonra POST isteğini oluşturalım. Metnin değiştirilmesini ücretsiz olarak hissetmekten çekinmeyin. Metnin kaçışlı olması gerekir.

```java
// This function performs a POST request.
public String Post() throws IOException {
    MediaType mediaType = MediaType.parse("application/json");
    RequestBody body = RequestBody.create(mediaType,
            "[{\n\t\"Text\": \"How are you? I am fine. What did you do today?\"\n}]");
    Request request = new Request.Builder()
            .url(url).post(body)
            .addHeader("Ocp-Apim-Subscription-Key", subscriptionKey)
            .addHeader("Content-type", "application/json").build();
    Response response = client.newCall(request).execute();
    return response.body().string();
}
```

## <a name="create-a-function-to-parse-the-response"></a>Yanıtı ayrıştırmak için bir işlev oluşturma

Bu basit işlev, Translator Metin Çevirisi hizmetinden gelen JSON yanıtını ayrıştırır ve önceden inceler.

```java
// This function prettifies the json response.
public static String prettify(String json_text) {
    JsonParser parser = new JsonParser();
    JsonElement json = parser.parse(json_text);
    Gson gson = new GsonBuilder().setPrettyPrinting().create();
    return gson.toJson(json);
}
```

## <a name="put-it-all-together"></a>Hepsini bir araya getirin

Son adım bir istek yapmak ve yanıt almak için kullanılır. Bu satırları projenize ekleyin:

```java
public static void main(String[] args) {
    try {
        BreakSentence breakSentenceRequest = new BreakSentence();
        String response = BreakSentenceRequest.Post();
        System.out.println(prettify(response));
    } catch (Exception e) {
        System.out.println(e);
    }
}
```

## <a name="run-the-sample-app"></a>Örnek uygulamayı çalıştırma

Bu, örnek uygulamanızı çalıştırmaya hazırsınız. Komut satırından (veya terminal oturumu), çalışma dizininizin köküne gidin ve şunu çalıştırın:

```console
gradle build
```

Oluşturma tamamlandığında, şunu çalıştırın:

```console
gradle run
```

## <a name="sample-response"></a>Örnek yanıt

Başarılı bir yanıt, aşağıdaki örnekte gösterildiği gibi JSON biçiminde döndürülür:

```json
[
  {
    "detectedLanguage": {
      "language": "en",
      "score": 1.0
    },
    "sentLen": [
      13,
      11,
      22
    ]
  }
]
```

## <a name="next-steps"></a>Sonraki adımlar

Translator Metin Çevirisi API'si ile yapabileceğiniz her şeyi anlamak için API başvurusuna göz atın.

> [!div class="nextstepaction"]
> [API başvurusu](https://docs.microsoft.com/azure/cognitive-services/translator/reference/v3-0-reference)
