---
title: Kubernetes config ve Deploy adımları Dil Algılama
titleSuffix: Azure Cognitive Services
description: Kubernetes config ve Deploy adımları Dil Algılama
services: cognitive-services
author: IEvangelist
manager: nitinme
ms.service: cognitive-services
ms.topic: include
ms.date: 09/19/2019
ms.author: dapine
ms.openlocfilehash: e3051a72a115e711a99ecd68756967e2cef0cc04
ms.sourcegitcommit: 2ed6e731ffc614f1691f1578ed26a67de46ed9c2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71130043"
---
### <a name="deploy-the-language-detection-container-to-an-aks-cluster"></a>Dil Algılama kapsayıcısını bir AKS kümesine dağıtma

1. Azure CLı 'yi açın ve Azure 'da oturum açın.

    ```azurecli
    az login
    ```

1. AKS kümesinde oturum açın. `your-cluster-name` Ve`your-resource-group` değerlerini uygun değerlerle değiştirin.

    ```azurecli
    az aks get-credentials -n your-cluster-name -g -your-resource-group
    ```

    Bu komut çalıştıktan sonra şuna benzer bir ileti bildirir:

    ```console
    Merged "your-cluster-name" as current context in /home/username/.kube/config
    ```

    > [!WARNING]
    > Azure hesabınızda kullanabileceğiniz birden çok aboneliğiniz varsa ve `az aks get-credentials` komut bir hatayla döndürülürse, yaygın bir sorun, yanlış aboneliği kullanıyor olmanız olabilir. Azure CLı oturumunuzun bağlamını, kaynaklarını oluşturduğunuz aboneliğin aynısını kullanacak şekilde ayarlayın ve yeniden deneyin.
    > ```azurecli
    >  az account set -s subscription-id
    > ```

1. İstediğiniz metin düzenleyicisini açın. Bu örnek Visual Studio Code kullanır.

    ```azurecli
    code .
    ```

1. Metin Düzenleyicisi içinde *Language. YAML*adlı yeni bir dosya oluşturun ve içine aşağıdaki YAML 'yi yapıştırın. `billing/value` Ve`apikey/value` bilgilerinizi kendi bilgileriniz ile değiştirdiğinizden emin olun.

    ```yaml
    apiVersion: apps/v1beta1
    kind: Deployment
    metadata:
      name: language
    spec:
      template:
        metadata:
          labels:
            app: language-app
        spec:
          containers:
          - name: language
            image: mcr.microsoft.com/azure-cognitive-services/language
            ports:
            - containerPort: 5000
            env:
            - name: EULA
              value: "accept"
            - name: billing
              value: # {ENDPOINT_URI}
            - name: apikey
              value: # {API_KEY}
     
    --- 
    apiVersion: v1
    kind: Service
    metadata:
      name: language
    spec:
      type: LoadBalancer
      ports:
      - port: 5000
      selector:
        app: language-app
    ```

1. Dosyayı kaydedin ve metin düzenleyicisini kapatın.
1. Kubernetes `apply` komutunu *Language. YAML* dosyası ile hedef olarak çalıştırın:

    ```console
    kuberctl apply -f language.yaml
    ```

    Komut, dağıtım yapılandırmasını başarılı bir şekilde uyguladıktan sonra aşağıdaki çıktıya benzer bir ileti görünür:

    ```console
    deployment.apps "language" created
    service "language" created
    ```
1. Pod 'ın dağıtıldığını doğrulayın:

    ```console
    kubectl get pods
    ```

    Pod 'un çalışma durumunun çıkışı:

    ```console
    NAME                         READY     STATUS    RESTARTS   AGE
    language-5c9ccdf575-mf6k5   1/1       Running   0          1m
    ```

1. Hizmetin kullanılabilir olduğunu doğrulayın ve IP adresini alın.

    ```console
    kubectl get services
    ```

    Pod 'daki *dil* hizmetinin çalışma durumunun çıkışı:

    ```console
    NAME         TYPE           CLUSTER-IP    EXTERNAL-IP      PORT(S)          AGE
    kubernetes   ClusterIP      10.0.0.1      <none>           443/TCP          2m
    language     LoadBalancer   10.0.100.64   168.61.156.180   5000:31234/TCP   2m
    ```
