---
title: Öğretici-kod işlemede görüntü oluşturma-Azure Container Registry görevler
description: Bu öğreticide, bir git deposuna kaynak kodu kaydederken buluttaki kapsayıcı görüntüsü yapılarını otomatik olarak tetiklemek üzere bir Azure Container Registry görevinin nasıl yapılandırılacağını öğreneceksiniz.
services: container-registry
author: dlepow
manager: gwallace
ms.service: container-registry
ms.topic: tutorial
ms.date: 05/04/2019
ms.author: danlep
ms.custom: seodec18, mvc
ms.openlocfilehash: d01863979f4cf74d544ef2b1ff121022abb8d4f6
ms.sourcegitcommit: a10074461cf112a00fec7e14ba700435173cd3ef
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73931435"
---
# <a name="tutorial-automate-container-image-builds-in-the-cloud-when-you-commit-source-code"></a>Öğretici: kaynak kodu kaydederken bulutta kapsayıcı görüntüsü derlemelerini otomatikleştirin

[Hızlı bir göreve](container-registry-tutorial-quick-task.md)ek olarak, ACR görevleri, kaynak kodu bir git deposuna kaydederken buluttaki otomatik Docker kapsayıcı görüntüsü derlemelerini destekler.

Bu öğreticide, ACR göreviniz bir git deposuna kaynak kodu kaydederken bir Dockerfile içinde belirtilen tek bir kapsayıcı görüntüsü oluşturur ve gönderir. Kod işlemede birden çok kapsayıcıyı oluşturma, gönderme ve isteğe bağlı olarak test etme adımlarını tanımlamak üzere YAML dosyası kullanan [çok adımlı bir görev](container-registry-tasks-multi-step.md) oluşturmak için bkz. [öğretici: kaynak kodu kaydederken bulutta çok adımlı bir kapsayıcı iş akışını çalıştırma](container-registry-tutorial-multistep-task.md). ACR görevlerine genel bakış için bkz. [ACR görevleri ile işletim sistemi ve çatı düzeltme ekini otomatikleştirme](container-registry-tasks-overview.md)

Bu öğreticide:

> [!div class="checklist"]
> * Görev oluşturma
> * Görevi test etme
> * Görev durumunu görüntüleme
> * Kod işlemesi ile görevi tetikleme

Bu öğreticide, [önceki öğreticide](container-registry-tutorial-quick-task.md) yer alan adımları zaten tamamladığınız varsayılır. Henüz yapmadıysanız, devam etmeden önce önceki öğreticinin [Önkoşullar](container-registry-tutorial-quick-task.md#prerequisites) bölümündeki adımları tamamlayın.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Azure CLı 'yı yerel olarak kullanmak istiyorsanız, [az Login][az-login]Ile Azure CLI sürüm **2.0.46** veya sonraki bir sürümünün yüklü ve oturum açmış olması gerekir. Sürümü bulmak için `az --version` komutunu çalıştırın. CLı 'yi yüklemeniz veya yükseltmeniz gerekiyorsa bkz. [Azure CLI 'Yı yüklemek][azure-cli].

[!INCLUDE [container-registry-task-tutorial-prereq.md](../../includes/container-registry-task-tutorial-prereq.md)]

## <a name="create-the-build-task"></a>Derleme görevi oluşturma

ACR Görevlerinin işleme durumunu okumasını etkinleştirmek ve bir depoda web kancaları oluşturmak için gereken adımları tamamladıktan sonra, depoya işleme yapılması üzerine kapsayıcı görüntüsü derlemesini tetikleyen bir görev oluşturabilirsiniz.

İlk olarak, bu kabuk ortam değişkenlerini ortamınıza uygun değerlerle doldurun. Bu adımın yapılması kesinlikle zorunlu değildir ancak bu öğreticideki çok satırlı Azure CLI komutlarını yürütmeyi biraz daha kolaylaştırır. Bu ortam değişkenlerini doldurmazsanız, her değeri örnek komutlarda göründüğü her yerde el ile değiştirmelisiniz.

```azurecli-interactive
ACR_NAME=<registry-name>        # The name of your Azure container registry
GIT_USER=<github-username>      # Your GitHub user account name
GIT_PAT=<personal-access-token> # The PAT you generated in the previous section
```

Şimdi aşağıdaki [az ACR Task Create][az-acr-task-create] komutunu yürüterek görevi oluşturun:

```azurecli-interactive
az acr task create \
    --registry $ACR_NAME \
    --name taskhelloworld \
    --image helloworld:{{.Run.ID}} \
    --context https://github.com/$GIT_USER/acr-build-helloworld-node.git \
    --file Dockerfile \
    --git-access-token $GIT_PAT
```

> [!IMPORTANT]
> Daha önce `az acr build-task` komutuyla önizleme sırasında görevler oluşturduysanız, bu görevlerin [az ACR Task][az-acr-task] komutu kullanılarak yeniden oluşturulması gerekir.

Bu görev, *ile belirtilen depodaki*ana`--context` dala kod işlenen her durumda ACR Görevlerinin söz konusu daldaki koddan kapsayıcı görüntüsü derleyeceğini belirtir. Depo kökünden `--file` tarafından belirtilen Dockerfile, görüntüyü oluşturmak için kullanılır. `--image` bağımsız değişkeni, görüntü etiketinin sürüm kısmı için parametreli `{{.Run.ID}}` değeri belirtir ve derlenen görüntünün belirli bir derleme ile ilişkili olmasını ve benzersiz şekilde etiketlenmesini sağlar.

Başarılı bir [az ACR görev oluştur][az-acr-task-create] komutunun çıktısı aşağıdakine benzer:

```console
{
  "agentConfiguration": {
    "cpu": 2
  },
  "creationDate": "2018-09-14T22:42:32.972298+00:00",
  "id": "/subscriptions/<Subscription ID>/resourceGroups/myregistry/providers/Microsoft.ContainerRegistry/registries/myregistry/tasks/taskhelloworld",
  "location": "westcentralus",
  "name": "taskhelloworld",
  "platform": {
    "architecture": "amd64",
    "os": "Linux",
    "variant": null
  },
  "provisioningState": "Succeeded",
  "resourceGroup": "myregistry",
  "status": "Enabled",
  "step": {
    "arguments": [],
    "baseImageDependencies": null,
    "contextPath": "https://github.com/gituser/acr-build-helloworld-node",
    "dockerFilePath": "Dockerfile",
    "imageNames": [
      "helloworld:{{.Run.ID}}"
    ],
    "isPushEnabled": true,
    "noCache": false,
    "type": "Docker"
  },
  "tags": null,
  "timeout": 3600,
  "trigger": {
    "baseImageTrigger": {
      "baseImageTriggerType": "Runtime",
      "name": "defaultBaseimageTriggerName",
      "status": "Enabled"
    },
    "sourceTriggers": [
      {
        "name": "defaultSourceTriggerName",
        "sourceRepository": {
          "branch": "master",
          "repositoryUrl": "https://github.com/gituser/acr-build-helloworld-node",
          "sourceControlAuthProperties": null,
          "sourceControlType": "GitHub"
        },
        "sourceTriggerEvents": [
          "commit"
        ],
        "status": "Enabled"
      }
    ]
  },
  "type": "Microsoft.ContainerRegistry/registries/tasks"
}
```

## <a name="test-the-build-task"></a>Derleme görevini test etme

Artık derlemenizi tanımlayan bir göreviniz var. Derleme ardışık düzenini test etmek için [az ACR Task Run][az-acr-task-run] komutunu yürüterek bir derlemeyi el ile tetikleyin:

```azurecli-interactive
az acr task run --registry $ACR_NAME --name taskhelloworld
```

Varsayılan olarak, `az acr task run` komutunu yürüttüğünüzde komut, günlük çıktısını konsolunuza akışla aktarır.

```console
$ az acr task run --registry $ACR_NAME --name taskhelloworld

2018/09/17 22:51:00 Using acb_vol_9ee1f28c-4fd4-43c8-a651-f0ed027bbf0e as the home volume
2018/09/17 22:51:00 Setting up Docker configuration...
2018/09/17 22:51:02 Successfully set up Docker configuration
2018/09/17 22:51:02 Logging in to registry: myregistry.azurecr.io
2018/09/17 22:51:03 Successfully logged in
2018/09/17 22:51:03 Executing step: build
2018/09/17 22:51:03 Obtaining source code and scanning for dependencies...
2018/09/17 22:51:05 Successfully obtained source code and scanned for dependencies
Sending build context to Docker daemon  23.04kB
Step 1/5 : FROM node:9-alpine
9-alpine: Pulling from library/node
Digest: sha256:8dafc0968fb4d62834d9b826d85a8feecc69bd72cd51723c62c7db67c6dec6fa
Status: Image is up to date for node:9-alpine
 ---> a56170f59699
Step 2/5 : COPY . /src
 ---> 5f574fcf5816
Step 3/5 : RUN cd /src && npm install
 ---> Running in b1bca3b5f4fc
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN helloworld@1.0.0 No repository field.

up to date in 0.078s
Removing intermediate container b1bca3b5f4fc
 ---> 44457db20dac
Step 4/5 : EXPOSE 80
 ---> Running in 9e6f63ec612f
Removing intermediate container 9e6f63ec612f
 ---> 74c3e8ea0d98
Step 5/5 : CMD ["node", "/src/server.js"]
 ---> Running in 7382eea2a56a
Removing intermediate container 7382eea2a56a
 ---> e33cd684027b
Successfully built e33cd684027b
Successfully tagged myregistry.azurecr.io/helloworld:da2
2018/09/17 22:51:11 Executing step: push
2018/09/17 22:51:11 Pushing image: myregistry.azurecr.io/helloworld:da2, attempt 1
The push refers to repository [myregistry.azurecr.io/helloworld]
4a853682c993: Preparing
[...]
4a853682c993: Pushed
[...]
da2: digest: sha256:c24e62fd848544a5a87f06ea60109dbef9624d03b1124bfe03e1d2c11fd62419 size: 1366
2018/09/17 22:51:21 Successfully pushed image: myregistry.azurecr.io/helloworld:da2
2018/09/17 22:51:21 Step id: build marked as successful (elapsed time in seconds: 7.198937)
2018/09/17 22:51:21 Populating digests for step id: build...
2018/09/17 22:51:22 Successfully populated digests for step id: build
2018/09/17 22:51:22 Step id: push marked as successful (elapsed time in seconds: 10.180456)
The following dependencies were found:
- image:
    registry: myregistry.azurecr.io
    repository: helloworld
    tag: da2
    digest: sha256:c24e62fd848544a5a87f06ea60109dbef9624d03b1124bfe03e1d2c11fd62419
  runtime-dependency:
    registry: registry.hub.docker.com
    repository: library/node
    tag: 9-alpine
    digest: sha256:8dafc0968fb4d62834d9b826d85a8feecc69bd72cd51723c62c7db67c6dec6fa
  git:
    git-head-revision: 68cdf2a37cdae0873b8e2f1c4d80ca60541029bf


Run ID: da2 was successful after 27s
```

## <a name="trigger-a-build-with-a-commit"></a>İşleme ile derleme tetikleme

Görevi el ile çalıştırarak test ettikten sonra, bir kaynak kodu değişikliği ile otomatik olarak tetikleyin.

İlk olarak, [deponun][sample-repo]yerel kopyasını içeren dizinde olduğunuzdan emin olun:

```azurecli-interactive
cd acr-build-helloworld-node
```

Ardından, yeni bir dosya oluşturmak, işlemek ve GitHub üzerindeki depo çatalınıza göndermek için aşağıdaki komutları yürütün:

```azurecli-interactive
echo "Hello World!" > hello.txt
git add hello.txt
git commit -m "Testing ACR Tasks"
git push origin master
```

`git push` komutunu yürüttüğünüzde GitHub kimlik bilgilerinizi sağlamanız istenebilir. GitHub kullanıcı adınızı sağlayın ve parola için daha önce oluşturduğunuz kişisel erişim belirtecini (PAT) girin.

```console
$ git push origin master
Username for 'https://github.com': <github-username>
Password for 'https://githubuser@github.com': <personal-access-token>
```

Bir işlemeyi deponuza gönderdikten sonra, ACR Görevleri tarafından oluşturulan web kancası başlatılır ve Azure Container Registry’de bir derleme başlatır. Derlemenin ilerleme durumunu doğrulamak ve izlemek için o anda devam eden görevin günlüklerini görüntüleyin:

```azurecli-interactive
az acr task logs --registry $ACR_NAME
```

Çıktı aşağıdakine benzer ve o anda yürütülen (veya son yürütülen) görevi gösterir:

```console
$ az acr task logs --registry $ACR_NAME
Showing logs of the last created run.
Run ID: da4

[...]

Run ID: da4 was successful after 38s
```

## <a name="list-builds"></a>Derlemeleri listeleme

Kayıt defteriniz için ACR görevlerinin tamamladığı görev çalıştırmalarının listesini görmek için [az ACR Task List-çalıştırmaları][az-acr-task-list-runs] komutunu çalıştırın:

```azurecli-interactive
az acr task list-runs --registry $ACR_NAME --output table
```

Komut çıktısı aşağıdakine benzer şekilde görünmelidir. ACR Görevlerinin yürüttüğü çalıştırmalar gösterilir ve en son görev için TRIGGER sütununda "Git İşleme" ifadesi görünür:

```console
$ az acr task list-runs --registry $ACR_NAME --output table

RUN ID    TASK             PLATFORM    STATUS     TRIGGER     STARTED               DURATION
--------  --------------  ----------  ---------  ----------  --------------------  ----------
da4       taskhelloworld  Linux       Succeeded  Git Commit  2018-09-17T23:03:45Z  00:00:44
da3       taskhelloworld  Linux       Succeeded  Manual      2018-09-17T22:55:35Z  00:00:35
da2       taskhelloworld  Linux       Succeeded  Manual      2018-09-17T22:50:59Z  00:00:32
da1                       Linux       Succeeded  Manual      2018-09-17T22:29:59Z  00:00:57
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, bir Git deposuna kaynak kodu işlediğinizde Azure’da kapsayıcı görüntü derlemelerini otomatik olarak tetiklemek üzere bir görev kullanmayı öğrendiniz. Bir kapsayıcı görüntüsünün temel görüntüsü güncelleştirildiğinde derlemeleri tetikleyen görevler oluşturmak için sonraki öğreticiye geçin.

> [!div class="nextstepaction"]
> [Temel görüntü güncelleştirmesi ile derlemeleri otomatikleştirme](container-registry-tutorial-base-image-update.md)

<!-- LINKS - External -->
[sample-repo]: https://github.com/Azure-Samples/acr-build-helloworld-node

<!-- LINKS - Internal -->
[azure-cli]: /cli/azure/install-azure-cli
[az-acr-task]: /cli/azure/acr/task
[az-acr-task-create]: /cli/azure/acr/task#az-acr-task-create
[az-acr-task-run]: /cli/azure/acr/task#az-acr-task-run
[az-acr-task-list-runs]: /cli/azure/acr/task#az-acr-task-list-runs
[az-login]: /cli/azure/reference-index#az-login



