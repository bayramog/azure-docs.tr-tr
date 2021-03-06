---
title: 'Öğretici: IBM Kenexa anket Enterprise ile Azure Active Directory Tümleştirmesi | Microsoft Docs'
description: Azure Active Directory ve IBM Kenexa anket kuruluş arasında çoklu oturum açmayı yapılandırmayı öğrenin.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 03/08/2019
ms.author: jeedes
ms.openlocfilehash: c649b966b3e210f6b026b06a9654761e0f97aea1
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/13/2019
ms.locfileid: "67099050"
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a>Öğretici: IBM Kenexa anket Enterprise ile Azure Active Directory Tümleştirmesi

Bu öğreticide, Azure Active Directory (Azure AD) ile IBM Kenexa anket Kurumsal tümleştirme konusunda bilgi edinin.
Azure AD ile IBM Kenexa anket Kurumsal tümleştirme ile aşağıdaki avantajları sağlar:

* IBM Kenexa anket Kurumsal erişimi, Azure AD'de kontrol edebilirsiniz.
* Azure AD hesaplarına otomatik olarak (çoklu oturum açma) için IBM Kenexa anket Kurumsal oturum açmış, kullanıcıların etkinleştirebilirsiniz.
* Hesaplarınız bir merkezi konumda - Azure portalında yönetebilir.

Azure AD SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz. [uygulama erişimi ve Azure Active Directory ile çoklu oturum açma nedir](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap oluşturun](https://azure.microsoft.com/free/).

## <a name="prerequisites"></a>Önkoşullar

Azure AD Tümleştirmesi ile IBM Kenexa anket Enterprise yapılandırmak için aşağıdaki öğeler gerekir:

* Azure AD aboneliğiniz. Bir Azure AD ortamını yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/)
* IBM Kenexa anket Kurumsal çoklu oturum açma abonelik etkin.

## <a name="scenario-description"></a>Senaryo açıklaması

Bu öğreticide, yapılandırma ve Azure AD çoklu oturum açma bir test ortamında test edin.

* IBM Kenexa anket Kurumsal destekler **IDP** tarafından başlatılan

## <a name="adding-ibm-kenexa-survey-enterprise-from-the-gallery"></a>IBM Kenexa anket Kurumsal galeri ekleme

Azure AD'de IBM Kenexa anket Kurumsal tümleştirmesini yapılandırmak için IBM Kenexa anket Kurumsal Galeriden yönetilen SaaS uygulamaları listesine eklemeniz gerekir.

**Galeriden IBM Kenexa anket kuruluş eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde **[Azure portalında](https://portal.azure.com)** , sol gezinti panelinde tıklayın **Azure Active Directory** simgesi.

    ![Azure Active Directory düğmesi](common/select-azuread.png)

2. Gidin **kurumsal uygulamalar** seçip **tüm uygulamaları** seçeneği.

    ![Kurumsal uygulamalar dikey penceresi](common/enterprise-applications.png)

3. Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmındaki düğmesi.

    ![Yeni Uygulama düğmesi](common/add-new-app.png)

4. Arama kutusuna **IBM Kenexa anket Kurumsal**seçin **IBM Kenexa anket Kurumsal** sonucu panelinden ardından **Ekle** uygulama eklemek için Ekle düğmesine.

     ![Sonuç listesinde IBM Kenexa anket Enterprise](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma IBM Kenexa anket adlı bir test kullanıcı tabanlı Kurumsal test **Britta Simon**.
Tek iş için oturum açma için bir Azure AD kullanıcısı ile IBM Kenexa anket Kurumsal ilgili kullanıcı arasında bir bağlantı ilişki kurulması gerekir.

Yapılandırma ve Azure AD çoklu oturum açma IBM Kenexa anket Enterprise ile test etmek için aşağıdaki yapı taşlarını tamamlanması gerekir:

1. **[Azure AD çoklu oturum açmayı yapılandırmayı](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[IBM Kenexa anket Kurumsal çoklu oturum açmayı yapılandırma](#configure-ibm-kenexa-survey-enterprise-single-sign-on)**  - uygulama tarafında çoklu oturum açma ayarlarını yapılandırmak için.
3. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.
4. **[Azure AD test kullanıcı atama](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açmayı kullanmak Britta Simon etkinleştirmek için.
5. **[IBM Kenexa anket Kurumsal test kullanıcısı oluşturma](#create-ibm-kenexa-survey-enterprise-test-user)**  - kullanıcı Azure AD gösterimini bağlı IBM Kenexa anket Enterprise'da Britta simon'un bir karşılığı vardır.
6. **[Çoklu oturum açmayı test](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin.

Azure AD çoklu oturum açma ile IBM Kenexa anket Enterprise yapılandırmak için aşağıdaki adımları gerçekleştirin:

1. İçinde [Azure portalında](https://portal.azure.com/), **IBM Kenexa anket Kurumsal** uygulama tümleştirme sayfasında **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma](common/select-sso.png)

2. Üzerinde **tek bir oturum açma yönteminizi seçmeniz** iletişim kutusunda, **SAML/WS-Federasyon** modu, çoklu oturum açmayı etkinleştirmek için.

    ![Çoklu oturum açma seçim modu](common/select-saml-option.png)

3. Üzerinde **yukarı çoklu oturum açma SAML ile ayarlanmış** sayfasında **Düzenle** açmak için simgeyi **temel SAML yapılandırma** iletişim.

    ![Temel SAML yapılandırmasını düzenle](common/edit-urls.png)

4. Üzerinde **yukarı çoklu oturum açma SAML ile ayarlanmış** sayfasında, aşağıdaki adımları gerçekleştirin:

    ![IBM Kenexa anket Kurumsal etki alanı ve URL'ler tek oturum açma bilgileri](common/idp-intiated.png)

    a. İçinde **tanımlayıcı** metin kutusuna şu biçimi kullanarak bir URL yazın: `https://surveys.kenexa.com/<companycode>`

    b. İçinde **yanıt URL'si** metin kutusuna şu biçimi kullanarak bir URL yazın: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    > [!NOTE]
    > Bu değerler gerçek değildir. Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin. İlgili kişi [IBM Kenexa anket Kurumsal İstemci Destek ekibine](https://www.ibm.com/support/home/?lnk=fcw) bu değerleri almak için. Gösterilen desenleri de başvurabilirsiniz **temel SAML yapılandırma** bölümünde Azure portalında.

5. IBM Kenexa anket Kurumsal uygulama, güvenlik onaylama işaretleme dili (SAML) onaylar SAML belirteci öznitelikleri yapılandırmanız için özel öznitelik eşlemelerini eklemeyi gerektiren belirli bir biçimde almak bekliyor. Yanıt kullanıcı tanımlayıcısı talep değerini Kenexa sisteminde yapılandırılmış SSO kimliği ile eşleşmelidir. Kuruluşunuzdaki SSO Internet Veri Birimi Protokolü (IDP) olarak uygun kullanıcı tanımlayıcısı eşlemek için çalışmak [IBM Kenexa anket Kurumsal Destek ekibine](https://www.ibm.com/support/home/?lnk=fcw).

    Varsayılan olarak, Azure AD Kullanıcı tanımlayıcısı kullanıcı asıl adı (UPN) değerini ayarlar. Bu değeri değiştirebilirsiniz **kullanıcı öznitelikleri** sekmesinde, aşağıdaki ekran görüntüsünde gösterildiği gibi. Tümleştirme çalışır yalnızca eşlemeyi tamamladıktan sonra doğru.

    ![image](common/edit-attribute.png)

6. Üzerinde **yukarı çoklu oturum açma SAML ile ayarlanmış** sayfasında **SAML imzalama sertifikası** bölümünde **indirme** indirmek için **sertifika (Base64)** bilgisayarınızdaki belirli seçenekler ihtiyacınıza göre ve kaydedin.

    ![Sertifika indirme bağlantısı](common/certificatebase64.png)

7. Üzerinde **IBM Kenexa anket Kurumsal kümesi** bölümünde, ihtiyacınıza göre uygun URL'lerini kopyalayın.

    ![Yapılandırma URL'leri kopyalayın](common/copy-configuration-urls.png)

    a. Oturum Açma URL'si:

    b. Azure AD Tanımlayıcısı

    c. Oturum Kapatma URL'si

### <a name="configure-ibm-kenexa-survey-enterprise-single-sign-on"></a>IBM Kenexa anket Kurumsal çoklu oturum açmayı yapılandırın

Çoklu oturum açmayı yapılandırma **IBM Kenexa anket Kurumsal** tarafı, indirilen göndermek için ihtiyacınız **sertifika (Base64)** ve uygun Azure portalına kopyalanan URL'lerden [IBM Kenexa Kurumsal Destek ekibine anket](https://www.ibm.com/support/home/?lnk=fcw). Bunlar, her iki kenarı da düzgün ayarlandığından SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcısı oluşturmaktır.

1. Azure portalında, sol bölmede seçin **Azure Active Directory**seçin **kullanıcılar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantıları](common/users.png)

2. Seçin **yeni kullanıcı** ekranın üstünde.

    ![Yeni kullanıcı düğmesi](common/new-user.png)

3. Kullanıcı özellikleri, aşağıdaki adımları gerçekleştirin.

    ![Kullanıcı iletişim kutusu](common/user-properties.png)

    a. İçinde **adı** alana **BrittaSimon**.
  
    b. İçinde **kullanıcı adı** alan türü **brittasimon@yourcompanydomain.extension**  
    Örneğin, BrittaSimon@contoso.com

    c. Seçin **Show parola** onay kutusunu işaretleyin ve ardından parola kutusunda görüntülenen değeri yazın.

    d. **Oluştur**’a tıklayın.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atayın

Bu bölümde, Azure çoklu oturum açma kullanmak için IBM Kenexa anket Kurumsal erişim vererek Britta Simon etkinleştirin.

1. Azure portalında **kurumsal uygulamalar**seçin **tüm uygulamaları**, ardından **IBM Kenexa anket Kurumsal**.

    ![Kurumsal uygulamalar dikey penceresi](common/enterprise-applications.png)

2. Uygulamalar listesinde **IBM Kenexa anket Kurumsal**.

    ![Uygulamalar listesinde IBM Kenexa anket Kurumsal bağlantı](common/all-applications.png)

3. Soldaki menüde **kullanıcılar ve gruplar**.

    !["Kullanıcılar ve Gruplar" bağlantısı](common/users-groups-blade.png)

4. Tıklayın **Kullanıcı Ekle** düğmesine ve ardından **kullanıcılar ve gruplar** içinde **atama Ekle** iletişim.

    ![Atama Ekle bölmesi](common/add-assign-user.png)

5. İçinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** 'a tıklayın kullanıcı listesinde **seçin** ekranın alt kısmındaki düğmesi.

6. SAML onaylaması ardından içinde herhangi bir rolü değer bekleniyor durumunda **rolü Seç** 'a tıklayın listeden bir kullanıcı için uygun rolü Seç iletişim kutusu **seçin** ekranın alt kısmındaki düğmesi.

7. İçinde **atama Ekle** iletişim tıklatın **atama** düğmesi.

### <a name="create-ibm-kenexa-survey-enterprise-test-user"></a>IBM Kenexa anket Kurumsal test kullanıcısı oluşturma

Bu bölümde, IBM Kenexa anket kuruluşta Britta Simon adlı bir kullanıcı oluşturun.

IBM Kenexa anket Kurumsal sistemde kullanıcı oluşturun ve SSO kimliği eşleştirebilirsiniz için çalışabileceğiniz [IBM Kenexa anket Kurumsal Destek ekibine](https://www.ibm.com/support/home/?lnk=fcw). Bu SSO kimlik değeri de Azure AD'den kullanıcı tanımlayıcısı değeri eşlenmelidir. Bu varsayılan ayarı değiştirebilirsiniz **özniteliği** sekmesi.

### <a name="test-single-sign-on"></a>Çoklu oturum açma testi

Bu bölümde, erişim panelini kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Erişim paneli IBM Kenexa anket Kurumsal kutucuğa tıkladığınızda, size otomatik olarak IBM Kenexa anket SSO'yu ayarlayın kuruluş oturum açmanız. Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Ek Kaynaklar

- [SaaS uygulamaları Azure Active Directory ile tümleştirme hakkında öğreticiler listesi](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Azure Active Directory ile uygulama erişimi ve çoklu oturum açma özellikleri nelerdir?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Azure Active Directory'de koşullu erişim nedir?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

