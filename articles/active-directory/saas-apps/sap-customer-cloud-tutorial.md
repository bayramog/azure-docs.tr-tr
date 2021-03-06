---
title: 'Öğretici: müşteri için SAP bulutu ile çoklu oturum açma (SSO) Tümleştirmesi Azure Active Directory | Microsoft Docs'
description: Müşteri için Azure Active Directory ve SAP bulutu arasında çoklu oturum açmayı nasıl yapılandıracağınızı öğrenin.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 09/20/2019
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 837787d375a7570b7daf0a149960ca0020bcdced
ms.sourcegitcommit: b4665f444dcafccd74415fb6cc3d3b65746a1a31
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72264028"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-sap-cloud-for-customer"></a>Öğretici: müşteri için SAP bulutu ile çoklu oturum açma (SSO) Tümleştirmesi Azure Active Directory

Bu öğreticide, Azure Active Directory (Azure AD) ile müşteri için SAP bulutunu tümleştirmeyi öğreneceksiniz. Müşteri için SAP Cloud 'ı Azure AD ile tümleştirdiğinizde şunları yapabilirsiniz:

* Azure AD 'de, müşteri için SAP bulutuna erişimi olan denetim.
* Kullanıcılarınızın Azure AD hesapları ile müşteri için SAP bulutuna otomatik olarak oturum açmalarına olanak sağlayın.
* Hesaplarınızı tek bir merkezi konumda yönetin-Azure portal.

Azure AD ile SaaS uygulaması tümleştirmesi hakkında daha fazla bilgi edinmek için bkz. [Azure Active Directory ile uygulama erişimi ve çoklu oturum açma nedir?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).

## <a name="prerequisites"></a>Önkoşullar

Başlamak için aşağıdaki öğeler gereklidir:

* Bir Azure AD aboneliği. Aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/)alabilirsiniz.
* Müşteri için SAP bulutu çoklu oturum açma (SSO) etkin abonelik.

## <a name="scenario-description"></a>Senaryo açıklaması

Bu öğreticide, Azure AD SSO 'yu bir test ortamında yapılandırıp test edersiniz.

* Müşteri için SAP bulutu, **SP** tarafından başlatılan SSO 'yu destekler

## <a name="adding-sap-cloud-for-customer-from-the-gallery"></a>Galeriden müşteri için SAP bulutu ekleme

Müşteri için SAP Cloud 'ın Azure AD 'ye tümleştirilmesini yapılandırmak için, Galeri 'den yönetilen SaaS uygulamaları listenize müşteri için SAP bulutu eklemeniz gerekir.

1. Bir iş veya okul hesabını ya da kişisel bir Microsoft hesabını kullanarak [Azure portalda](https://portal.azure.com) oturum açın.
1. Sol gezinti bölmesinde **Azure Active Directory** hizmeti ' ni seçin.
1. **Kurumsal uygulamalar** ' a gidin ve **tüm uygulamalar**' ı seçin.
1. Yeni uygulama eklemek için **Yeni uygulama**' yı seçin.
1. **Galeriden Ekle** bölümünde, arama kutusuna **müşteri için SAP Cloud** yazın.
1. Sonuçlar panelinden **Müşteri Için SAP bulutu** ' nı seçin ve ardından uygulamayı ekleyin. Uygulama kiracınıza eklenirken birkaç saniye bekleyin.

## <a name="configure-and-test-azure-ad-single-sign-on-for-sap-cloud-for-customer"></a>Müşteri için SAP bulutu için Azure AD çoklu oturum açmayı yapılandırma ve test etme

**B. Simon**adlı bir test kullanıcısı kullanarak Azure AD SSO 'yu MÜŞTERI Için SAP bulutu ile yapılandırın ve test edin. SSO 'nun çalışması için, bir Azure AD kullanıcısı ve müşteri için SAP bulutu 'ndaki ilgili Kullanıcı arasında bir bağlantı ilişkisi oluşturmanız gerekir.

Azure AD SSO 'yu müşteri için SAP bulutu ile yapılandırmak ve test etmek için aşağıdaki yapı taşlarını doldurun:

1. **[Azure AD SSO 'Yu yapılandırın](#configure-azure-ad-sso)** -kullanıcılarınızın bu özelliği kullanmasını sağlamak için.
    1. Azure AD **[test kullanıcısı oluşturun](#create-an-azure-ad-test-user)** -B. Simon Ile Azure AD çoklu oturum açma sınamasını test edin.
    1. Azure AD **[Test kullanıcısına atama](#assign-the-azure-ad-test-user)** -Azure AD çoklu oturum açma özelliğini kullanmak için B. Simon 'u etkinleştirmek için.
1. Uygulama tarafında çoklu oturum açma ayarlarını yapılandırmak için, **[Müşteri SSO 'su IÇIN SAP bulutu 'Nı yapılandırın](#configure-sap-cloud-for-customer-sso)** .
    1. Kullanıcının Azure AD gösterimine bağlı olan müşteriler için SAP bulutu 'nda B. Simon 'un bir karşılığı olacak şekilde, **[Müşteri IÇIN SAP bulutu oluşturun](#create-sap-cloud-for-customer-test-user)** .
1. **[Test SSO](#test-sso)** -yapılandırmanın çalışıp çalışmadığını doğrulamak için.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 'yu yapılandırma

Azure portal Azure AD SSO 'yu etkinleştirmek için bu adımları izleyin.

1. [Azure Portal](https://portal.azure.com/), **müşteri için SAP bulutu** uygulama tümleştirmesi sayfasında, **Yönet** bölümünü bulun ve **Çoklu oturum açma**' yı seçin.
1. **Çoklu oturum açma yöntemi seçin** sayfasında **SAML**' yi seçin.
1. **SAML ile çoklu oturum açmayı ayarlama** sayfasında, ayarları düzenlemek IÇIN **temel SAML yapılandırması** için Düzenle/kalem simgesine tıklayın.

   ![Temel SAML yapılandırmasını düzenle](common/edit-urls.png)

1. **Temel SAML yapılandırması** bölümünde, aşağıdaki alanlar için değerleri girin:

    a. **Oturum açma URL 'si** metin kutusunda, aşağıdaki kalıbı kullanarak bir URL yazın: `https://<server name>.crm.ondemand.com`

    b. **Tanımlayıcı (VARLıK kimliği)** metin kutusuna şu kalıbı kullanarak bir URL yazın: `https://<server name>.crm.ondemand.com`

    > [!NOTE]
    > Bu değerler gerçek değildir. Bu değerleri, gerçek oturum açma URL 'SI ve tanımlayıcısı ile güncelleştirin. Bu değerleri almak için [Müşteri Için SAP bulutu istemci desteği ekibine](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) başvurun. Ayrıca, Azure portal **temel SAML yapılandırması** bölümünde gösterilen desenlere de başvurabilirsiniz.

1. Müşteri için SAP Cloud uygulaması, SAML belirteci öznitelikleri yapılandırmanıza özel öznitelik eşlemeleri eklemenizi gerektiren belirli bir biçimde SAML onayları bekler. Aşağıdaki ekran görüntüsünde varsayılan özniteliklerin listesi gösterilmektedir. Kullanıcı öznitelikleri iletişim kutusunu açmak için **Düzenle** simgesine tıklayın.

    ![image](common/edit-attribute.png)

1. **Kullanıcı öznitelikleri & talepler** Iletişim kutusundaki **Kullanıcı öznitelikleri** bölümünde aşağıdaki adımları uygulayın:

    a. **Kullanıcı taleplerini Yönet** iletişim kutusunu açmak için **Düzenle simgesine** tıklayın.

    ![image](./media/sap-customer-cloud-tutorial/tutorial_usermail.png)

    ![image](./media/sap-customer-cloud-tutorial/tutorial_usermailedit.png)

    b. **Kaynak**olarak **dönüşüm** ' i seçin.

    c. **Dönüştürme** listesinden **Extractmailprefix ()** öğesini seçin.

    d. **Parametre 1** listesinden, uygulamanız için kullanmak istediğiniz kullanıcı özniteliğini seçin.
    Örneğin, EmployeeID 'yi benzersiz kullanıcı tanımlayıcısı olarak kullanmak istiyorsanız ve öznitelik değerini ExtensionAttribute2 içinde depoladıysanız User. ExtensionAttribute2 ' yi seçin.

    e. **Kaydet** düğmesine tıklayın.

1. **SAML ile çoklu oturum açmayı ayarlama** sayfasında, **SAML imzalama sertifikası** bölümünde, **Federasyon meta verileri XML** 'i bulun ve sertifikayı indirip bilgisayarınıza kaydetmek için **İndir** ' i seçin.

    ![Sertifika indirme bağlantısı](common/metadataxml.png)

1. **Müşteri IÇIN SAP Cloud ayarla** bölümünde, gereksiniminize göre uygun URL 'leri kopyalayın.

    ![Yapılandırma URL 'Lerini Kopyala](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Azure AD test kullanıcısı oluşturma

Bu bölümde, B. Simon adlı Azure portal bir test kullanıcısı oluşturacaksınız.

1. Azure portal sol bölmeden **Azure Active Directory**' i seçin, **Kullanıcılar**' ı seçin ve ardından **tüm kullanıcılar**' ı seçin.
1. Ekranın üst kısmındaki **Yeni Kullanıcı** ' yı seçin.
1. **Kullanıcı** özellikleri ' nde şu adımları izleyin:
   1. **Ad** alanına `B.Simon` girin.  
   1. **Kullanıcı adı** alanına username@companydomain.extension girin. Örneğin, `B.Simon@contoso.com`.
   1. **Parolayı göster** onay kutusunu seçin ve ardından **parola** kutusunda görüntülenen değeri yazın.
   1. **Oluştur**’a tıklayın.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD test kullanıcısını atama

Bu bölümde, müşteri için SAP buluta erişim vererek Azure çoklu oturum açma özelliğini kullanmak için B. Simon 'u etkinleştireceksiniz.

1. Azure portal **Kurumsal uygulamalar**' ı seçin ve ardından **tüm uygulamalar**' ı seçin.
1. Uygulamalar listesinde, **Müşteri Için SAP bulutu**' nı seçin.
1. Uygulamanın genel bakış sayfasında **Yönet** bölümünü bulun ve **Kullanıcılar ve gruplar**' ı seçin.

   !["Kullanıcılar ve gruplar" bağlantısı](common/users-groups-blade.png)

1. **Kullanıcı Ekle**' yi seçin, sonra **atama Ekle** iletişim kutusunda **Kullanıcılar ve gruplar** ' ı seçin.

    ![Kullanıcı Ekle bağlantısı](common/add-assign-user.png)

1. **Kullanıcılar ve gruplar** iletişim kutusunda, kullanıcılar listesinden **B. Simon** ' ı seçin ve ardından ekranın alt kısmındaki **Seç** düğmesine tıklayın.
1. SAML assertion 'da herhangi bir rol değeri bekliyorsanız, **Rol Seç** iletişim kutusunda, Kullanıcı için listeden uygun rolü seçin ve ardından ekranın alt kısmındaki **Seç** düğmesine tıklayın.
1. **Atama Ekle** Iletişim kutusunda **ata** düğmesine tıklayın.

## <a name="configure-sap-cloud-for-customer-sso"></a>Müşteri SSO 'SU için SAP bulutu yapılandırma

1. Yeni bir Web tarayıcı penceresi açın ve müşteri için SAP Cloud şirket sitenizde yönetici olarak oturum açın.

2. Menünün sol tarafında, **kimlik sağlayıcıları**  @ no__t-2**şirket kimliği sağlayıcıları** > **Ekle** ' ye tıklayın ve açılır pencerede **Azure AD**gibi kimlik sağlayıcısı adını ekleyin, **Kaydet** ' e tıklayın ve ardından SAML ' ye tıklayın.  **2,0 yapılandırma**.

    ![SAP yapılandırması](./media/sap-customer-cloud-tutorial/configure01.png)

3. **SAML 2,0 yapılandırma** bölümünde aşağıdaki adımları uygulayın:

    ![SAP yapılandırması](./media/sap-customer-cloud-tutorial/configure02.png)

    a. Azure portal 'ten indirdiğiniz Federasyon meta veri XML dosyasını karşıya yüklemek için, **Araştır** ' a tıklayın.

    b. XML dosyası başarıyla karşıya yüklendikten sonra, aşağıdaki değerler otomatik olarak doldurulur ve **Kaydet**' e tıklayın.

### <a name="create-sap-cloud-for-customer-test-user"></a>Müşteri için SAP bulutu test kullanıcısı oluşturma

Azure AD kullanıcılarının müşteri için SAP bulutu 'nda oturum açmasını sağlamak için, müşteri için SAP Cloud 'a sağlanması gerekir. Müşteri için SAP bulutu 'nda sağlama işlemi el ile gerçekleştirilen bir görevdir.

**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**

1. Bir güvenlik yöneticisi olarak müşteri için SAP bulutu 'nda oturum açın.

2. Menünün sol tarafında **kullanıcılar & yetkilendirmeler**  @ no__t-2 **Kullanıcı yönetimi** > **Kullanıcı Ekle**' ye tıklayın.

    ![SAP yapılandırması](./media/sap-customer-cloud-tutorial/configure03.png)

3. **Yeni Kullanıcı Ekle** bölümünde aşağıdaki adımları uygulayın:

    ![SAP yapılandırması](./media/sap-customer-cloud-tutorial/configure04.png)

    a. **Ad** metin kutusuna **B**gibi kullanıcının adını girin.

    b. **Soyadı** metin kutusuna **Simon**gibi kullanıcının adını girin.

    c. **E-posta** metin kutusuna `B.Simon@contoso.com` gibi kullanıcının e-postasını girin.

    d. **Oturum açma adı** metin kutusuna **B. Simon**gibi kullanıcının adını girin.

    e. Gereksiniminize göre **Kullanıcı türü** ' nü seçin.

    f. Gereksiniminize göre **hesap etkinleştirme** seçeneğini belirleyin.

## <a name="test-sso"></a>Test SSO 'SU 

Bu bölümde, erişim panelini kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edersiniz.

Erişim panelinde müşteri için SAP bulutu kutucuğuna tıkladığınızda, SSO 'yu ayarladığınız müşteri için SAP bulutu 'nda otomatik olarak oturum açmış olmanız gerekir. Erişim paneli hakkında daha fazla bilgi için bkz. [erişim paneline giriş](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Ek kaynaklar

- [SaaS uygulamalarını Azure Active Directory ile tümleştirme hakkında öğreticiler listesi](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Azure Active Directory ile uygulama erişimi ve çoklu oturum açma nedir?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Azure Active Directory Koşullu erişim nedir?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Azure AD ile müşteri için SAP bulutu 'nı deneyin](https://aad.portal.azure.com/)

