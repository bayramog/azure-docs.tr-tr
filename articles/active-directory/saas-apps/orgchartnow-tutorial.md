---
title: 'Öğretici: Kuruluş Şeması artık Azure Active Directory tümleştirmesiyle | Microsoft Docs'
description: Azure Active Directory ve Kuruluş Şeması şimdi arasında çoklu oturum açmayı yapılandırmayı öğrenin.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 50a1522f-81de-4d14-9b6b-dd27bb1338a4
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 03/14/2019
ms.author: jeedes
ms.openlocfilehash: b96606b5558e0fbb81733b2f548a89bfb38d5f99
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/13/2019
ms.locfileid: "67095442"
---
# <a name="tutorial-azure-active-directory-integration-with-orgchart-now"></a>Öğretici: Kuruluş Şeması şimdi ile Azure Active Directory Tümleştirme

Bu öğreticide, Kuruluş Şeması artık Azure Active Directory (Azure AD) ile tümleştirmeyi öğrenin.
Kuruluş Şeması şimdi Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:

* Kuruluş Şeması şimdi erişimi, Azure AD'de kontrol edebilirsiniz.
* Azure AD hesaplarına otomatik olarak (çoklu oturum açma) için Kuruluş Şeması şimdi oturum açmış, kullanıcıların etkinleştirebilirsiniz.
* Hesaplarınız bir merkezi konumda - Azure portalında yönetebilir.

Azure AD SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz. [uygulama erişimi ve Azure Active Directory ile çoklu oturum açma nedir](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap oluşturun](https://azure.microsoft.com/free/).

## <a name="prerequisites"></a>Önkoşullar

Kuruluş Şeması artık Azure AD tümleştirmesini yapılandırmak için aşağıdaki öğeler gerekir:

* Azure AD aboneliğiniz. Bir Azure AD ortamını yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/)
* Kuruluş Şeması şimdi çoklu oturum açma abonelik etkin.

## <a name="scenario-description"></a>Senaryo açıklaması

Bu öğreticide, yapılandırma ve Azure AD çoklu oturum açma bir test ortamında test edin.

* Kuruluş Şeması şimdi destekler **SP** ve **IDP** tarafından başlatılan

## <a name="adding-orgchart-now-from-the-gallery"></a>Kuruluş Şeması şimdi galeri ekleme

Kuruluş Şeması artık Azure AD'de tümleştirmesini yapılandırmak için Kuruluş Şeması şimdi Galeriden yönetilen SaaS uygulamaları listesine eklemeniz gerekir.

**Kuruluş Şeması şimdi Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde **[Azure portalında](https://portal.azure.com)** , sol gezinti panelinde tıklayın **Azure Active Directory** simgesi.

    ![Azure Active Directory düğmesi](common/select-azuread.png)

2. Gidin **kurumsal uygulamalar** seçip **tüm uygulamaları** seçeneği.

    ![Kurumsal uygulamalar dikey penceresi](common/enterprise-applications.png)

3. Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmındaki düğmesi.

    ![Yeni Uygulama düğmesi](common/add-new-app.png)

4. Arama kutusuna **Kuruluş Şeması şimdi**seçin **Kuruluş Şeması şimdi** sonucu panelinden ardından **Ekle** uygulama eklemek için Ekle düğmesine.

     ![Kuruluş Şeması artık sonuçlar listesinde](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırmanız ve Kuruluş Şeması şimdi ile Azure AD çoklu oturum açmayı test adlı bir test kullanıcı tabanlı **Britta Simon**.
Tek iş için oturum açma için bir Azure AD kullanıcı ve Kuruluş Şeması şimdi ilgili kullanıcı arasında bir bağlantı ilişki kurulması gerekir.

Yapılandırma ve Azure AD çoklu oturum açma Kuruluş Şeması şimdi ile test etmek için aşağıdaki yapı taşlarını tamamlanması gerekir:

1. **[Azure AD çoklu oturum açmayı yapılandırmayı](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[Kuruluş Şeması artık çoklu oturum açmayı yapılandırma](#configure-orgchart-now-single-sign-on)**  - uygulama tarafında çoklu oturum açma ayarlarını yapılandırmak için.
3. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.
4. **[Azure AD test kullanıcı atama](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açmayı kullanmak Britta Simon etkinleştirmek için.
5. **[Kuruluş Şeması şimdi test kullanıcısı oluşturma](#create-orgchart-now-test-user)**  - kullanıcı Azure AD gösterimini bağlı kuruluş şeması şimdi Britta simon'un bir karşılığı vardır.
6. **[Çoklu oturum açmayı test](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin.

Azure AD çoklu oturum açma ile Kuruluş Şeması şimdi yapılandırmak için aşağıdaki adımları gerçekleştirin:

1. İçinde [Azure portalında](https://portal.azure.com/), **Kuruluş Şeması şimdi** uygulama tümleştirme sayfasında **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma](common/select-sso.png)

2. Üzerinde **tek bir oturum açma yönteminizi seçmeniz** iletişim kutusunda, **SAML/WS-Federasyon** modu, çoklu oturum açmayı etkinleştirmek için.

    ![Çoklu oturum açma seçim modu](common/select-saml-option.png)

3. Üzerinde **yukarı çoklu oturum açma SAML ile ayarlanmış** sayfasında **Düzenle** açmak için simgeyi **temel SAML yapılandırma** iletişim.

    ![Temel SAML yapılandırmasını düzenle](common/edit-urls.png)

4. Üzerinde **temel SAML yapılandırma** uygulamada yapılandırmak isterseniz, bölümü **IDP** modunda başlatılan aşağıdaki adımı uygulayın:

    ![Kuruluş Şeması artık etki alanı ve URL'ler tek oturum açma bilgileri](common/idp-identifier.png)

    İçinde **tanımlayıcı** metin kutusuna bir URL yazın:  `https://sso2.orgchartnow.com`

5. Tıklayın **ek URL'lerini ayarlayın** ve uygulamada yapılandırmak istiyorsanız, aşağıdaki adımı uygulayın **SP** başlatılan modu:

    ![image](common/both-preintegrated-signon.png)

    İçinde **oturum açma URL'si** metin kutusuna şu biçimi kullanarak bir URL yazın:  `https://sso2.orgchartnow.com/Shibboleth.sso/Login?entityID=<YourEntityID>&target=https://sso2.orgchartnow.com`

    > [!NOTE]
    > `<YourEntityID>` olan **Azure AD tanımlayıcısı** kopyalanmış **ayarlayın Kuruluş Şeması şimdi** bölümünde, bu öğreticinin sonraki bölümlerinde açıklanan.

6. Üzerinde **yukarı çoklu oturum açma SAML ile ayarlanmış** sayfasında **SAML imzalama sertifikası** bölümünde **indirme** indirmek için **Federasyon meta veri XML**  bilgisayarınızdaki belirli seçenekler ihtiyacınıza göre ve kaydedin.

    ![Sertifika indirme bağlantısı](common/metadataxml.png)

7. Üzerinde **ayarlayın Kuruluş Şeması şimdi** bölümünde, ihtiyacınıza göre uygun URL'lerini kopyalayın.

    ![Yapılandırma URL'leri kopyalayın](common/copy-configuration-urls.png)

    a. Oturum Açma URL'si:

    b. Azure AD Tanımlayıcısı

    c. Oturum Kapatma URL'si

### <a name="configure-orgchart-now-single-sign-on"></a>Kuruluş Şeması şimdi çoklu oturum açmayı yapılandırın

Çoklu oturum açmayı yapılandırma **Kuruluş Şeması şimdi** tarafı, indirilen göndermek için ihtiyacınız **Federasyon meta verileri XML** ve uygun kopyalanan URL'ler için Azure portalından [Kuruluş Şeması şimdi destek ekibi ](mailto:ocnsupport@officeworksoftware.com). Bunlar, her iki kenarı da düzgün ayarlandığından SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.

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

Bu bölümde, Azure çoklu oturum açma kullanmak için Kuruluş Şeması şimdi erişim vererek Britta Simon etkinleştirin.

1. Azure portalında **kurumsal uygulamalar**seçin **tüm uygulamaları**, ardından **Kuruluş Şeması şimdi**.

    ![Kurumsal uygulamalar dikey penceresi](common/enterprise-applications.png)

2. Uygulamalar listesinde **Kuruluş Şeması şimdi**.

    ![Kuruluş Şeması şimdi bağlantısına uygulamalar listesinde](common/all-applications.png)

3. Soldaki menüde **kullanıcılar ve gruplar**.

    !["Kullanıcılar ve Gruplar" bağlantısı](common/users-groups-blade.png)

4. Tıklayın **Kullanıcı Ekle** düğmesine ve ardından **kullanıcılar ve gruplar** içinde **atama Ekle** iletişim.

    ![Atama Ekle bölmesi](common/add-assign-user.png)

5. İçinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** 'a tıklayın kullanıcı listesinde **seçin** ekranın alt kısmındaki düğmesi.

6. SAML onaylaması ardından içinde herhangi bir rolü değer bekleniyor durumunda **rolü Seç** 'a tıklayın listeden bir kullanıcı için uygun rolü Seç iletişim kutusu **seçin** ekranın alt kısmındaki düğmesi.

7. İçinde **atama Ekle** iletişim tıklatın **atama** düğmesi.

### <a name="create-orgchart-now-test-user"></a>Kuruluş Şeması şimdi test kullanıcısı oluşturma

Azure AD kullanıcıları için Kuruluş Şeması şimdi oturum açmayı etkinleştirmek için bunların Kuruluş Şeması şimdi sağlanması gerekir. 

1. Kuruluş Şeması şimdi tam zamanında sağlama, varsayılan olarak etkin olan destekler. Yeni bir kullanıcı, henüz yoksa, Kuruluş Şeması şimdi erişme denemesi sırasında oluşturulur. Sağlama özelliğini tam zamanında kullanıcı yalnızca oluşturacak bir **salt okunur** kullanıcıya bir SSO isteği tanınan IDP'den gelir ve SAML onayı e-postada kullanıcı listesinde bulunamadı. Başlıklı bir erişim grubu oluşturmak gereken bu otomatik sağlama için **genel** Kuruluş Şeması şimdi. Lütfen bir erişim grubu oluşturmak için aşağıdaki adımları:

    a. Git **grupları yönet** tıkladıktan sonra seçeneği **dişli** sağ üst köşesindeki kullanıcı Arabirimi içinde.

    ![Kuruluş Şeması şimdi grupları](./media/orgchartnow-tutorial/tutorial_orgchartnow_manage.png)    

    b. Seçin **Ekle** simgesi ve grubun adı **genel** ardından **Tamam**. 

    ![Kuruluş Şeması şimdi ekleyin](./media/orgchartnow-tutorial/tutorial_orgchartnow_add.png)

    c. Genel veya salt okunur kullanıcı erişebilmesi için istediğiniz klasörleri seçin:

    ![Kuruluş Şeması şimdi klasörleri](./media/orgchartnow-tutorial/tutorial_orgchartnow_chart.png)

    d. **Kilit** klasörleri yalnızca yönetici kullanıcılar bunları değiştirebilir. Tuşuna basarak **Tamam**.

    ![Kuruluş Şeması şimdi Kilitle](./media/orgchartnow-tutorial/tutorial_orgchartnow_lock.png)

2. Oluşturulacak **yönetici** kullanıcılar ve **okuma/yazma** kullanıcıları, el ile oluşturmanız gerekir bir kullanıcı kendi ayrıcalık düzeyi SSO aracılığıyla erişmek için. Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:

    a. İçin Kuruluş Şeması artık bir güvenlik yöneticisi olarak oturum açın.

    b.  Tıklayarak **ayarları** sağ üst köşe ve ardından gidin **Kullanıcıları Yönet**.

    ![Kuruluş Şeması şimdi ayarları](./media/orgchartnow-tutorial/tutorial_orgchartnow_settings.png)

    c. Tıklayarak **Ekle** ve aşağıdaki adımları gerçekleştirin:

    ![Kuruluş Şeması şimdi yönetme](./media/orgchartnow-tutorial/tutorial_orgchartnow_manageusers.png)

    * İçinde **kullanıcı kimliği** metin kullanıcı kimliği gibi girin **brittasimon\@contoso.com**.

    * İçinde **e-posta adresi** metin kutusuna, kullanıcının gibi e-posta girin **brittasimon\@contoso.com**.

    * **Ekle**'yi tıklatın.

### <a name="test-single-sign-on"></a>Çoklu oturum açma testi 

Bu bölümde, erişim panelini kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Erişim paneli Kuruluş Şeması şimdi kutucuğa tıkladığınızda, size otomatik olarak SSO'yu ayarlayın Kuruluş Şeması şimdi için oturum açmanız. Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Ek Kaynaklar

- [SaaS uygulamaları Azure Active Directory ile tümleştirme hakkında öğreticiler listesi](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Azure Active Directory ile uygulama erişimi ve çoklu oturum açma özellikleri nelerdir?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Azure Active Directory'de koşullu erişim nedir?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

