---
title: Azure HDInsight Spark kümesinde işleri göndermek için Livy Spark kullanma
description: Bir Azure HDInsight kümesinde Spark işleri uzaktan göndermek için Apache Spark REST API'sini kullanmayı öğrenin.
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 06/11/2019
ms.openlocfilehash: f5b3500e1e700abf894fc4e21fb540eb258d5e35
ms.sourcegitcommit: 41ca82b5f95d2e07b0c7f9025b912daf0ab21909
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/13/2019
ms.locfileid: "67066069"
---
# <a name="use-apache-spark-rest-api-to-submit-remote-jobs-to-an-hdinsight-spark-cluster"></a>Apache Spark uzak bir HDInsight Spark kümesine göndermek için REST API kullanma

Nasıl kullanacağınızı öğrenin [Apache Livy](https://livy.incubator.apache.org/), [Apache Spark](https://spark.apache.org/) REST API, uzak bir Azure HDInsight Spark kümesine göndermek için kullanılır. Ayrıntılı belgeler için bkz. [ https://livy.incubator.apache.org/ ](https://livy.incubator.apache.org/).

Etkileşimli Spark Kabukları çalıştırmak veya Spark üzerinde çalıştırılacak toplu iş göndermek için Livy kullanabilirsiniz. Bu makalede, toplu işleri göndermek için Livy kullanma hakkında konuşuyor. Bu makalede kod parçacıkları, Livy Spark uç noktası için REST API çağrıları gerçekleştirmek için cURL kullanın.

## <a name="prerequisites"></a>Önkoşullar

* HDInsight üzerinde bir Apache Spark kümesi. Yönergeler için bkz. [Azure HDInsight'ta Apache Spark kümeleri oluşturma](apache-spark-jupyter-spark-sql.md).

* [cURL](https://curl.haxx.se/). Bu makalede, bir HDInsight Spark kümesine göre REST API çağrılarının nasıl yapılacağını göstermek üzere cURL kullanılmıştır.

## <a name="submit-an-apache-livy-spark-batch-job"></a>Bir Apache Livy Spark batch işi gönderme

Batch işi göndermeden önce uygulama jar kümeyle ilişkili küme depolama alanına yüklemeniz gerekir. Kullanabileceğiniz [AzCopy](../../storage/common/storage-use-azcopy.md), bunu yapmak için bir komut satırı yardımcı. Verileri yüklemek için kullanabileceğiniz çeşitli istemciler vardır. Onları hakkında daha fazla bulabilirsiniz [HDInsight Apache Hadoop işleri için verileri karşıya yükleme](../hdinsight-upload-data.md).

```cmd
curl -k --user "<hdinsight user>:<user password>" -v -H "Content-Type: application/json" -X POST -d '{ "file":"<path to application jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches' -H "X-Requested-By: admin"
```

### <a name="examples"></a>Örnekler

* Jar dosyasını küme depolama (WASB) ise

    ```cmd  
    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches" -H "X-Requested-By: admin"
    ```

* Jar dosya adı ve classname giriş dosyası bir parçası olarak geçirilecek isterseniz (Bu örnekte, input.txt)

    ```cmd
    curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches" -H "X-Requested-By: admin"
    ```

## <a name="get-information-on-livy-spark-batches-running-on-the-cluster"></a>Küme üzerinde çalışan Livy Spark toplu işlemler hakkında bilgi edinin

Sözdizimi:

```cmd
curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"
```

### <a name="examples"></a>Örnekler

* Tüm küme üzerinde çalışan Livy Spark toplu almak istiyorsanız:

    ```cmd
    curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches" 
    ```

* Belirtilen toplu iş kimliği ile belirli bir batch almak istiyorsanız

    ```cmd
    curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"
    ```

## <a name="delete-a-livy-spark-batch-job"></a>Livy Spark toplu silme

```cmd
curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"
```

### <a name="example"></a>Örnek

Toplu iş kimliği ile bir batch işi siliniyor `5`.

```cmd
curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/5"
```

## <a name="livy-spark-and-high-availability"></a>Livy Spark ve yüksek kullanılabilirlik

Livy yüksek kullanılabilirlik için Spark kümesinde çalışan işleri sağlar. Aşağıda birkaç örnek verilmiştir.

* Uzaktan bir Spark kümesi için bir işi gönderdikten sonra Livy hizmet arıza yaparsa, iş, arka planda çalışmaya devam eder. Livy yedekleme olduğunda geri raporları ve iş durumunu geri yükler.
* HDInsight için Jupyter not defterleri ile arka uçtaki Livy tarafından desteklenir. Livy hizmeti yeniden ve bir not defteri bir Spark işi çalıştığından, Not Defteri, kod hücreleri çalışmaya devam eder. 

## <a name="show-me-an-example"></a>Örneği Göster

Bu bölümde, batch işi gönderme, işinin ilerleme durumunu izlemek ve silin Livy Spark'ta kullanmak için örneklere bakacağız. Bu örnekte kullandığımız makalesinde geliştirilen bir uygulamadır [Scala uygulama tek başına bir HDInsight Spark kümesi üzerinde oluşturup](apache-spark-create-standalone-application.md). Buradaki adımları istediğinizi düşünelim:

* Ayrıca, kümeyle ilişkili depolama hesabına zaten uygulama jar kopyaladınız.
* CuRL, şu adımları çalıştığınız bilgisayarda yüklü var.

Aşağıdaki adımları gerçekleştirin:

1. Bize Livy Spark kümesinde çalıştığını ilk doğrulayın. Biz bunu çalışan toplu işler listesini alarak yapabilirsiniz. Livy kullanarak ilk kez bir işi çalıştırıyorsanız, sıfır çıkış döndürmelidir.

    ```cmd
    curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
    ```

    Aşağıdaki kod parçacığına benzer bir çıktı almalısınız:

    ```output
    < HTTP/1.1 200 OK
    < Content-Type: application/json; charset=UTF-8
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Fri, 20 Nov 2015 23:47:53 GMT
    < Content-Length: 34
    <
    {"from":0,"total":0,"sessions":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
    ```

    Çıkış son satırında ne diyor fark **toplam: 0**, hiçbir çalışan toplu işler önerir.

2. Bize bir batch işi şimdi gönderin. Aşağıdaki kod parçacığı jar adı ve sınıf adı, parametre olarak geçirmek için bir giriş dosyası (input.txt) kullanır. Bu adımları bir Windows bilgisayardan çalıştırılıyorsa, giriş dosyası kullanılması önerilen yaklaşımdır.

    ```cmd
    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches" -H "X-Requested-By: admin"
    ```

    Parametreler dosyasındaki **input.txt** şu şekilde tanımlanır:

    ```text
    { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
    ```

    Aşağıdaki kod parçacığına benzer bir çıktı görmeniz gerekir:

    ```output
    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /0
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Fri, 20 Nov 2015 23:51:30 GMT
    < Content-Length: 36
    <
    {"id":0,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
    ```

    Çıkış son satırının ne diyor fark **durumu: Başlangıç**. Ayrıca diyor, **kimliği: 0**. Burada, **0** toplu işlem kimliğidir.

3. Şimdi toplu iş kimliğini kullanarak bu belirli toplu işlem durumunu Al

    ```cmd
    curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
    ```

    Aşağıdaki kod parçacığına benzer bir çıktı görmeniz gerekir:

    ```output
    < HTTP/1.1 200 OK
    < Content-Type: application/json; charset=UTF-8
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Fri, 20 Nov 2015 23:54:42 GMT
    < Content-Length: 509
    <
    {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
    ```

    Şimdi çıktısında **durumu: başarılı**, kullandınız. işi başarıyla tamamlandı.

4. Batch, artık isterseniz silebilirsiniz.

    ```cmd
    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
    ```

    Aşağıdaki kod parçacığına benzer bir çıktı görmeniz gerekir:

    ```output
    < HTTP/1.1 200 OK
    < Content-Type: application/json; charset=UTF-8
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Sat, 21 Nov 2015 18:51:54 GMT
    < Content-Length: 17
    <
    {"msg":"deleted"}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
    ```

    Çıkışının son satırında batch başarıyla silindiğini gösterir. Bir iş çalışır durumdayken silme işi sonlandırır. Bir iş, başarıyla veya aksi halde tamamlandı silerseniz iş bilgilerini tamamen siler.

## <a name="updates-to-livy-configuration-starting-with-hdinsight-35-version"></a>HDInsight 3.5 sürümünden başlayarak Livy yapılandırma güncelleştirmeleri

HDInsight 3.5 kümeleri ve varsayılan olarak, yukarıdaki erişim örnek veri dosyalarını veya jar dosyaları dışındaki yerel dosya yolları kullanımını devre dışı. Kullanmanızı öneriyoruz `wasb://` yolu yerine jar dosyaları dışındaki erişmek veya örnek veri dosyalarını kümeden.

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a>Livy işleri bir küme içinde bir Azure sanal ağı için gönderme

Bir Azure sanal ağ içindeki bir HDInsight Spark kümesine bağlanıyorsanız, küme üzerinde Livy için doğrudan bağlantı kurabilir. Böyle bir durumda, Livy uç nokta URL'si şudur `http://<IP address of the headnode>:8998/batches`. Burada, **8998** Livy çalıştığı küme baş düğüme bağlantı noktasıdır. Genel olmayan bağlantı noktalarında hizmetlerine erişme hakkında daha fazla bilgi için bkz: [HDInsight üzerinde Apache Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları](../hdinsight-hadoop-port-settings-for-services.md).

## <a name="next-steps"></a>Sonraki adımlar

* [Apache Livy REST API belgeleri](https://livy.incubator.apache.org/docs/latest/rest-api.html)
* [Azure HDInsight’ta Apache Spark kümesi kaynaklarını yönetme](apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](apache-spark-job-debugging.md)