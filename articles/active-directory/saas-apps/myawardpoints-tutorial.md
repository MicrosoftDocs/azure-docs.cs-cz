---
title: 'Kurz: Azure Active Directory integrací s body ocenění nahoře/nejvyšším týmem | Microsoft Docs'
description: Přečtěte si, jak nakonfigurovat jednotné přihlašování mezi Azure Active Directory a v horním nebo horním týmu bodů ocenění.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 03/01/2019
ms.author: jeedes
ms.openlocfilehash: f2328bd51712089f706c8491007f9f51eba52337
ms.sourcegitcommit: 59f506857abb1ed3328fda34d37800b55159c91d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/24/2020
ms.locfileid: "92508056"
---
# <a name="tutorial-azure-active-directory-integration-with-my-award-points-top-subtop-team"></a>Kurz: Azure Active Directory integrací s body ocenění nahoru a týmem nahoře

V tomto kurzu se dozvíte, jak v Azure Active Directory (Azure AD) integrovat hlavní a horní tým pro body ocenění.
Integrace bodů ocenění Top sub/Top tým s Azure AD poskytuje následující výhody:

* Můžete kontrolovat v Azure AD, kteří mají přístup k hlavnímu nebo hornímu týmu bodů ocenění.
* Můžete uživatelům povolit, aby se automaticky přihlásili k mým koncovým a horním týmu (jednotné přihlašování) k účtům Azure AD.
* Účty můžete spravovat v jednom centrálním umístění – Azure Portal.

Pokud chcete získat další podrobnosti o integraci aplikace SaaS s Azure AD, přečtěte si téma [co je přístup k aplikacím a jednotné přihlašování pomocí Azure Active Directory](../manage-apps/what-is-single-sign-on.md).
Pokud předplatné Azure ještě nemáte, napřed si [vytvořte bezplatný účet](https://azure.microsoft.com/free/).

## <a name="prerequisites"></a>Předpoklady

K nakonfigurování integrace služby Azure AD s nejvyšším dílčím a horním týmem pro body ocenění potřebujete následující položky:

* Předplatné služby Azure AD. Pokud nemáte prostředí Azure AD, můžete získat měsíční zkušební verzi [tady](https://azure.microsoft.com/pricing/free-trial/) .
* Moje ocenění v horním/horním týmu s povoleným jednorázovým přihlášením

## <a name="scenario-description"></a>Popis scénáře

V tomto kurzu nakonfigurujete a otestujete jednotné přihlašování Azure AD v testovacím prostředí.

* V horním a horním týmu pro body ocenění je podporována aktualizace SSO iniciovaná v **SP**

## <a name="adding-my-award-points-top-subtop-team-from-the-gallery"></a>Z Galerie se přidávají hlavní dílčí a hlavní tým pro body ocenění

Pokud chcete v rámci služby Azure AD nakonfigurovat integraci mých hlavních a nejvyšších bodů ocenění do Azure AD, musíte z Galerie přidat své body ocenění Top sub a top Team do seznamu spravovaných aplikací SaaS.

**Pokud chcete z Galerie přidat body ocenění nahoru a nahoru, proveďte následující kroky:**

1. V **[Azure Portal](https://portal.azure.com)** na levém navigačním panelu klikněte na ikonu **Azure Active Directory** .

    ![Tlačítko Azure Active Directory](common/select-azuread.png)

2. Přejděte na **podnikové aplikace** a vyberte možnost **všechny aplikace** .

    ![Okno podnikové aplikace](common/enterprise-applications.png)

3. Chcete-li přidat novou aplikaci, klikněte na tlačítko **Nová aplikace** v horní části dialogového okna.

    ![Tlačítko Nová aplikace](common/add-new-app.png)

4. Do vyhledávacího pole zadejte text **body ocenění nahoře sub/Top Team**, vyberte z panelu výsledků možnost **body ocenění horní/horní tým** a potom kliknutím na tlačítko **Přidat** přidejte aplikaci.

     ![V seznamu výsledků mají hlavní tým a body ocenění nahoře podřízený tým](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurace a testování jednotného přihlašování Azure AD

V této části nakonfigurujete a otestujete jednotné přihlašování Azure AD s body ocenění v horním nebo horním týmu na základě testovacího uživatele s názvem **Britta Simon**.
Aby jednotné přihlašování fungovalo, musí být navázán odkaz na odkaz mezi uživatelem služby Azure AD a souvisejícím uživatelem v mých dílčích a nejvyšších fázích Award.

Pokud chcete nakonfigurovat a otestovat jednotné přihlašování Azure AD pomocí nejdůležitějších dílčích a nejvyšších bodů ocenění, je nutné dokončit následující stavební bloky:

1. **[Nakonfigurujte jednotné přihlašování Azure AD](#configure-azure-ad-single-sign-on)** a Umožněte uživatelům používat tuto funkci.
2. Pokud chcete konfigurovat nastavení jednoho Sign-On na straně aplikace, **nakonfigurujte v horním nebo horním rámci týmu jednotné přihlašování** .
3. **[Vytvořte testovacího uživatele Azure AD](#create-an-azure-ad-test-user)** – k otestování jednotného přihlašování Azure AD pomocí Britta Simon.
4. **[Přiřaďte testovacího uživatele Azure AD](#assign-the-azure-ad-test-user)** – pro povolení Britta Simon pro použití jednotného přihlašování Azure AD.
5. Vytvořte si hlavní a horní tým **testovacích bodů pro uživatele** , kteří mají protějšek Britta Simon v seznamu mých ocenění v horním/horním týmu, který se odkazuje na reprezentaci uživatele v Azure AD.
6. **[Otestujte jednotné přihlašování](#test-single-sign-on)** – ověřte, jestli konfigurace funguje.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurace jednotného přihlašování Azure AD

V této části povolíte jednotné přihlašování Azure AD v Azure Portal.

Pokud chcete nakonfigurovat jednotné přihlašování pomocí služby Azure AD v horním nebo horním týmu bodů ocenění, proveďte následující kroky:

1. V [Azure Portal](https://portal.azure.com/)na stránce **Moje ocenění nahoře sub/Top Team** Application Integration, vyberte **jednotné přihlašování**.

    ![Konfigurovat odkaz jednotného přihlašování](common/select-sso.png)

2. V dialogovém okně **Vyberte metodu jednotného přihlašování** vyberte možnost režim **SAML/WS** , čímž povolíte jednotné přihlašování.

    ![Režim výběru jednotného přihlašování](common/select-saml-option.png)

3. Na stránce **nastavit jeden Sign-On s SAML** klikněte na **Upravit** ikona a otevře se základní dialogové okno **Konfigurace SAML** .

    ![Upravit základní konfiguraci SAML](common/edit-urls.png)

4. V části **základní konfigurace SAML** proveďte následující kroky:

    ![Informace o jednotném přihlašování v hlavních/horních týmových doménách a adresách URL](common/sp-signonurl.png)

    Do textového pole **přihlašovací adresa URL** zadejte adresu URL pomocí následujícího vzoru:  `https://microsoftrr.performnet.com/biwv1auth/Shibboleth.sso/Login?providerId=<Azure AD Identifier>`

    > [!NOTE]
    > Hodnota není reálné číslo. Tuto `<Azure AD Identifier>` hodnotu získáte v pozdějších krocích tohoto kurzu.

5. Na stránce **nastavit jeden Sign-On se** stránkou SAML v části **podpisový certifikát SAML** klikněte na **Stáhnout** a Stáhněte si **XML federačních metadat** z daných možností podle vašich požadavků a uložte ho do svého počítače.

    ![Odkaz na stažení certifikátu](common/metadataxml.png)

6. V části **nastavení bodů ocenění nahoře a v nejvyšším týmu** zkopírujte příslušné adresy URL podle vašich požadavků. 

    ![Kopírovat adresy URL konfigurace](common/copy-configuration-urls.png)

    a. Přihlašovací adresa URL

    b. Identifikátor Azure AD

    c. Odhlašovací adresa URL

    >[!NOTE]
    >Na místo `<Azure AD Identifier>` v části **základní konfigurace SAML** v Azure Portal připojit zkopírovanou hodnotu identifikátoru Azure AD s přihlašovací adresou URL.

### <a name="configure-my-award-points-top-subtop-team-single-sign-on"></a>Konfigurace hlavních a nejvyšších směrných míst pro jeden Sign-On týmu

Ke konfiguraci jednotného přihlašování na straně **začátku a horního týmu pro body ocenění** je potřeba odeslat stažená **metadata federačních metadat** a příslušné zkopírované adresy URL z Azure Portal na [tým podpory v horním nebo horním](mailto:myawardpoints@biworldwide.com)týmu. Toto nastavení nastaví, aby bylo správně nastaveno připojení SAML SSO na obou stranách.

### <a name="create-an-azure-ad-test-user"></a>Vytvoření testovacího uživatele Azure AD 

Cílem této části je vytvořit testovacího uživatele v Azure Portal s názvem Britta Simon.

1. V Azure Portal v levém podokně vyberte možnost **Azure Active Directory**, vyberte možnost **Uživatelé**a potom vyberte možnost **Všichni uživatelé**.

    ![Odkazy "uživatelé a skupiny" a "Všichni uživatelé"](common/users.png)

2. V horní části obrazovky vyberte **Nový uživatel** .

    ![Tlačítko pro nového uživatele](common/new-user.png)

3. Ve vlastnostech uživatele proveďte následující kroky.

    ![Uživatelský dialog](common/user-properties.png)

    a. Do pole **název** zadejte **BrittaSimon**.
  
    b. Do pole **uživatelské jméno** zadejte **brittasimon \@ yourcompanydomain. extension.**  
    Například BrittaSimon@contoso.com.

    c. Zaškrtněte políčko **Zobrazit heslo** a pak zapište hodnotu, která se zobrazí v poli heslo.

    d. Klikněte na **Vytvořit**.

### <a name="assign-the-azure-ad-test-user"></a>Přiřazení testovacího uživatele Azure AD

V této části povolíte Britta Simon pro použití jednotného přihlašování pomocí Azure tím, že udělíte přístup k hornímu nebo hornímu týmu bodů ocenění.

1. V Azure Portal vyberte možnost **podnikové aplikace**, vyberte možnost **všechny aplikace**a pak vyberte možnost **body ocenění horní/horní tým**.

    ![Okno Podnikové aplikace](common/enterprise-applications.png)

2. V seznamu aplikace vyberte možnost **body ocenění horní dílčí/vrchní tým**.

    ![Odkaz na horní/horní tým pro body ocenění v seznamu aplikací](common/all-applications.png)

3. V nabídce na levé straně vyberte **Uživatelé a skupiny**.

    ![Odkaz uživatelé a skupiny](common/users-groups-blade.png)

4. Klikněte na tlačítko **Přidat uživatele** a pak v dialogovém okně **Přidat přiřazení** vyberte **Uživatelé a skupiny** .

    ![Podokno přidat přiřazení](common/add-assign-user.png)

5. V dialogovém okně **Uživatelé a skupiny** vyberte v seznamu uživatelé možnost **Britta Simon** a pak klikněte na tlačítko **Vybrat** v dolní části obrazovky.

6. Pokud očekáváte hodnotu role v kontrolním výrazu SAML, pak v dialogovém okně **Vybrat roli** vyberte v seznamu příslušnou roli pro uživatele a pak klikněte na tlačítko **Vybrat** v dolní části obrazovky.

7. V dialogovém okně **Přidat přiřazení** klikněte na tlačítko **přiřadit** .

### <a name="create-my-award-points-top-subtop-team-test-user"></a>Vytvořit body ocenění v horním/horním týmu testovacího uživatele

V této části vytvoříte uživatele s názvem Britta Simon v části body ocenění v horním nebo horním týmu. S využitím [týmových a nejaktivnějších pracovních bodů](mailto:myawardpoints@biworldwide.com) v oblasti mých odměn můžete přidat uživatele na přední hlavní platformě a na nejvyšší úrovni vaší společnosti. Před použitím jednotného přihlašování je nutné vytvořit a aktivovat uživatele.

### <a name="test-single-sign-on"></a>Test jednotného přihlašování 

V této části otestujete konfiguraci jednotného přihlašování Azure AD pomocí přístupového panelu.

Když na přístupovém panelu kliknete na dlaždici horních a nejvyšších bodů ocenění, měli byste být automaticky přihlášeni k hornímu a hornímu týmu bodů ocenění, pro který jste nastavili jednotné přihlašování. Další informace o přístupovém panelu najdete v tématu [Úvod do přístupového panelu](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Další zdroje

- [Seznam kurzů pro integraci aplikací SaaS s Azure Active Directory](./tutorial-list.md)

- [Jak ve službě Azure Active Directory probíhá přístup k aplikacím a jednotné přihlašování?](../manage-apps/what-is-single-sign-on.md)

- [Co je podmíněný přístup v Azure Active Directory?](../conditional-access/overview.md)