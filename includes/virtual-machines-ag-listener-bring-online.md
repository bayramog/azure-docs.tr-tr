---
author: cynthn
ms.service: virtual-machines
ms.topic: include
ms.date: 10/26/2018
ms.author: cynthn
ms.openlocfilehash: 760bb5b62e9bba9b7a83f99760f7fe5d8c399dfb
ms.sourcegitcommit: 3e98da33c41a7bbd724f644ce7dedee169eb5028
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67188322"
---
1. Yük Devretme Kümesi Yöneticisi'nde **rolleri**ve ardından, kullanılabilirlik grubunu vurgulayın.  

2. Üzerinde **kaynakları** sekmesinde dinleyici adına sağ tıklayın ve ardından **özellikleri**.

3. Tıklayın **bağımlılıkları** sekmesi. Birden çok kaynak listede yoksa, IP adresleri veya değil olduğunu doğrulayın ve bağımlılıkları.  

4. **Tamam** düğmesine tıklayın.

5. Dinleyici adına sağ tıklayın ve ardından **çevrimiçine**.

6. Dinleyici üzerindeki çevrimiçi olduktan sonra **kaynakları** sekmesinde kullanılabilirlik grubuna sağ tıklayın ve ardından **özellikleri**.
   
    ![Kullanılabilirlik grubu kaynağını Yapılandır](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. (IP adresi kaynakları adı değil) dinleyici adı kaynağına bağlı bir bağımlılık oluşturmak ve ardından **Tamam**.
   
    ![Dinleyici adına bağımlılık Ekle](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. SQL Server Management Studio'yu başlatın ve sonra birincil kopyaya bağlanın.

9. Git **AlwaysOn yüksek kullanılabilirlik** > **kullanılabilirlik grupları** >  **\<AvailabilityGroupName\>**   >  **Kullanılabilirlik grubu dinleyicisi**.  
    Yük Devretme Kümesi Yöneticisi'nde, oluşturduğunuz adlı dinleyiciyi görüntülenmesi gerekir.

10. Dinleyici adına sağ tıklayın ve ardından **özellikleri**.

11. İçinde **bağlantı noktası** kutusunda, daha önce kullandığınız $EndpointPort kullanarak için kullanılabilirlik grubu dinleyicisinin bağlantı noktası numarası belirtin (Bu öğreticide, varsayılan 1433 olduğu) ve ardından **Tamam**.

