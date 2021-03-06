---
title: 'Kurz: Azure Active Directory integraci jednotného přihlašování (SSO) s CyberSolutions MAILBASEΣ \ CMS | Microsoft Docs'
description: Přečtěte si, jak nakonfigurovat jednotné přihlašování mezi Azure Active Directory a CyberSolutions MAILBASEΣ \ CMS.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 09/09/2020
ms.author: jeedes
ms.openlocfilehash: 9a1bed217f12646687654f37145a4a796d0487a1
ms.sourcegitcommit: 9b8425300745ffe8d9b7fbe3c04199550d30e003
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/23/2020
ms.locfileid: "92454996"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-cybersolutions-mailbasecmss"></a>Kurz: Azure Active Directory integraci jednotného přihlašování (SSO) s CyberSolutions MAILBASEΣ \ CMS

V tomto kurzu se dozvíte, jak integrovat CyberSolutions MAILBASEΣ \ CMS s Azure Active Directory (Azure AD). Když integrujete CyberSolutions MAILBASEΣ \ CMS s Azure AD, můžete:

* Řízení ve službě Azure AD, která má přístup k CyberSolutions MAILBASEΣ \ CMS.
* Umožněte uživatelům, aby se automaticky přihlásili k CyberSolutions MAILBASEΣ \ CMS pomocí svých účtů Azure AD.
* Spravujte svoje účty v jednom centrálním umístění – Azure Portal.

## <a name="prerequisites"></a>Požadavky

Chcete-li začít, potřebujete následující položky:

* Předplatné služby Azure AD. Pokud předplatné nemáte, můžete získat [bezplatný účet](https://azure.microsoft.com/free/).
* CyberSolutions MAILBASEΣ \ CMS předplatné s povoleným jednotným přihlašováním (SSO).

## <a name="scenario-description"></a>Popis scénáře

V tomto kurzu nakonfigurujete a otestujete jednotné přihlašování Azure AD v testovacím prostředí.

* CyberSolutions MAILBASEΣ \ CMS podporuje **aktualizace SP a IDP** iniciované pro jednotné přihlašování

## <a name="adding-cybersolutions-mailbasecmss-from-the-gallery"></a>Přidání CyberSolutions MAILBASEΣ \ CMS z Galerie

Pokud chcete nakonfigurovat integraci CyberSolutions MAILBASEΣ \ CMS do Azure AD, musíte přidat CyberSolutions MAILBASEΣ \ CMS z Galerie do svého seznamu spravovaných aplikací SaaS.

1. Přihlaste se k Azure Portal pomocí pracovního nebo školního účtu nebo osobního účet Microsoft.
1. V levém navigačním podokně vyberte službu **Azure Active Directory** .
1. Přejděte na **podnikové aplikace** a pak vyberte **všechny aplikace**.
1. Chcete-li přidat novou aplikaci, vyberte možnost **Nová aplikace**.
1. V části **Přidat z Galerie** do vyhledávacího pole zadejte **CYBERSOLUTIONS MAILBASEΣ \ CMS** .
1. Vyberte **CYBERSOLUTIONS MAILBASEΣ \ CMS** z panelu výsledků a pak přidejte aplikaci. Počkejte několik sekund, než se aplikace přidá do vašeho tenanta.


## <a name="configure-and-test-azure-ad-sso-for-cybersolutions-mailbasecmss"></a>Konfigurace a testování jednotného přihlašování Azure AD pro CyberSolutions MAILBASEΣ \ CMS

Nakonfigurujte a otestujte jednotné přihlašování Azure AD pomocí CyberSolutions MAILBASEΣ \ CMS pomocí testovacího uživatele s názvem **B. Simon**. Aby jednotné přihlašování fungovalo, je potřeba vytvořit vztah propojení mezi uživatelem služby Azure AD a souvisejícím uživatelem v CyberSolutions MAILBASEΣ \ CMS.

Pokud chcete nakonfigurovat a otestovat jednotné přihlašování Azure AD pomocí CyberSolutions MAILBASEΣ \ CMS, dokončete následující stavební bloky:

1. **[NAKONFIGURUJTE jednotné přihlašování Azure AD](#configure-azure-ad-sso)** – umožníte uživatelům používat tuto funkci.
    1. **[Vytvořte testovacího uživatele Azure AD](#create-an-azure-ad-test-user)** – k otestování jednotného přihlašování Azure AD pomocí B. Simon.
    1. **[Přiřaďte testovacího uživatele Azure AD](#assign-the-azure-ad-test-user)** – Pokud chcete povolit B. Simon používat jednotné přihlašování Azure AD.
1. **[Nakonfigurujte CYBERSOLUTIONS MAILBASE SSO](#configure-cybersolutions-mailbase-sso)** – pro konfiguraci nastavení jednotného přihlašování na straně aplikace.
    1. **[Vytvořte MAILBASE testovacího uživatele CyberSolutions](#create-cybersolutions-mailbase-test-user)** , abyste měli protějšek B. Simon v CyberSolutions MAILBASEΣ \ CMS, která je propojená s reprezentací uživatele v Azure AD.
1. **[Test SSO](#test-sso)** – ověřte, zda konfigurace funguje.

## <a name="configure-azure-ad-sso"></a>Konfigurace jednotného přihlašování v Azure AD

Pomocí těchto kroků povolíte jednotné přihlašování služby Azure AD v Azure Portal.

1. V Azure Portal na stránce integrace aplikace **CYBERSOLUTIONS MAILBASEΣ \ CMS** najděte část **Správa** a vyberte **jednotné přihlašování**.
1. Na stránce **Vyberte metodu jednotného přihlašování** vyberte **SAML**.
1. Na stránce **nastavit jednotné přihlašování pomocí SAML** klikněte na ikonu Upravit/pero pro **základní konfiguraci SAML** a upravte nastavení.

   ![Upravit základní konfiguraci SAML](common/edit-urls.png)

1. Pokud chcete nakonfigurovat aplikaci v režimu iniciované **IDP** , zadejte v **základní části Konfigurace SAML** hodnoty následujících polí:

    a. Do textového pole **identifikátor** zadejte adresu URL pomocí následujícího vzoru: `https://<SUBDOMAIN>.cybercloud.jp/saml/module.php/saml/sp/metadata.php/mb_generic_sp`

    b. Do textového pole **Adresa URL odpovědi** zadejte adresu URL pomocí následujícího vzoru: `https://<SUBDOMAIN>.cybercloud.jp/cgi-bin/mbase/mblogin/saml2-acs/mb_generic_sp`

1. Klikněte na **nastavit další adresy URL** a proveďte následující krok, pokud chcete nakonfigurovat aplikaci v režimu iniciované **SP** :

    Do textového pole **přihlašovací adresa URL** zadejte adresu URL pomocí následujícího vzoru:  `https://<SUBDOMAIN>.cybercloud.jp/cgi-bin/mbase/mblogin?saml_domain=<domain>`

    > [!NOTE]
    > Tyto hodnoty nejsou reálné. Aktualizujte tyto hodnoty skutečným identifikátorem, adresou URL odpovědi a přihlašovací adresou URL. K získání těchto hodnot se obraťte na [tým podpory CYBERSOLUTIONS MAILBASEΣ \ CMS](mailto:tech@cybersolutions.co.jp) . Můžete se také podívat na vzory uvedené v části **základní konfigurace SAML** v Azure Portal.

1. Na stránce **nastavit jednotné přihlašování pomocí SAML** v části **podpisový certifikát SAML** Najděte **XML metadata federace** a vyberte **Stáhnout** a Stáhněte certifikát a uložte ho do svého počítače.

    ![Odkaz na stažení certifikátu](common/metadataxml.png)

1. V části **Nastavení CYBERSOLUTIONS MAILBASEΣ \ CMS** zkopírujte na základě vašeho požadavku příslušné adresy URL.

    ![Kopírovat adresy URL konfigurace](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Vytvoření testovacího uživatele Azure AD

V této části vytvoříte testovacího uživatele ve Azure Portal s názvem B. Simon.

1. V levém podokně Azure Portal vyberte možnost **Azure Active Directory**, vyberte možnost **Uživatelé**a potom vyberte možnost **Všichni uživatelé**.
1. V horní části obrazovky vyberte **Nový uživatel** .
1. Ve vlastnostech **uživatele** proveďte následující kroky:
   1. Do pole **Název** zadejte `B.Simon`.  
   1. Do pole **uživatelské jméno** zadejte username@companydomain.extension . Například, `B.Simon@contoso.com`.
   1. Zaškrtněte políčko **Zobrazit heslo** a pak zapište hodnotu, která se zobrazí v poli **heslo** .
   1. Klikněte na **Vytvořit**.

### <a name="assign-the-azure-ad-test-user"></a>Přiřazení testovacího uživatele Azure AD

V této části povolíte B. Simon používat jednotné přihlašování pomocí Azure tím, že udělíte přístup k CyberSolutions MAILBASEΣ \ CMS.

1. V Azure Portal vyberte **podnikové aplikace**a pak vyberte **všechny aplikace**.
1. V seznamu aplikace vyberte možnost **CYBERSOLUTIONS MAILBASEΣ \ CMS**.
1. Na stránce Přehled aplikace najděte část **Správa** a vyberte **Uživatelé a skupiny**.
1. Vyberte **Přidat uživatele**a pak v dialogovém okně **Přidat přiřazení** vyberte **Uživatelé a skupiny** .
1. V dialogovém okně **Uživatelé a skupiny** vyberte v seznamu uživatelé možnost **B. Simon** a pak klikněte na tlačítko **Vybrat** v dolní části obrazovky.
1. Pokud očekáváte, že role má být přiřazena uživatelům, můžete ji vybrat v rozevíracím seznamu **Vybrat roli** . Pokud pro tuto aplikaci není nastavená žádná role, zobrazí se vybraná role výchozí přístup.
1. V dialogovém okně **Přidat přiřazení** klikněte na tlačítko **přiřadit** .

## <a name="configure-cybersolutions-mailbase-sso"></a>Konfigurace jednotného přihlašování CyberSolutions MAILBASE

Ke konfiguraci jednotného přihlašování na straně **CYBERSOLUTIONS MAILBASEΣ \ CMS** je potřeba odeslat stažená **metadata federačních metadat** a příslušné zkopírované adresy URL z Azure Portal do [týmu podpory MAILBASEΣ CMS \](mailto:tech@cybersolutions.co.jp). Toto nastavení nastaví, aby bylo správně nastaveno připojení SAML SSO na obou stranách.

### <a name="create-cybersolutions-mailbase-test-user"></a>Vytvořit testovacího uživatele CyberSolutions MAILBASE

V této části vytvoříte uživatele s názvem Britta Simon v CyberSolutions MAILBASEΣ \ CMS. Pokud chcete přidat uživatele do platformy CyberSolutions MAILBASEΣ \ CMS, pracujte s [týmem podpory CYBERSOLUTIONS MAILBASEΣ \ CMS](mailto:tech@cybersolutions.co.jp) . Před použitím jednotného přihlašování je nutné vytvořit a aktivovat uživatele.

## <a name="test-sso"></a>Test SSO 

V této části otestujete konfiguraci jednotného přihlašování Azure AD pomocí následujících možností. 

#### <a name="sp-initiated"></a>Zahájena SP:

* Kliknutím na **test této aplikace** v Azure Portal. Tím se přesměruje na adresu URL CyberSolutions MAILBASEΣ \ CMS, kde můžete spustit tok přihlášení.  

* Přejít na adresu URL pro přihlášení k CyberSolutions MAILBASEΣ \ CMS a spustit tok přihlášení přímo z tohoto účtu.

#### <a name="idp-initiated"></a>Iniciované IDP:

* Klikněte na **testovat tuto aplikaci** v Azure Portal a měli byste se automaticky přihlášeni k CyberSolutions MAILBASEΣ \ CMS, pro kterou jste si nastavili jednotné přihlašování. 

K otestování aplikace v jakémkoli režimu můžete také použít panel Microsoft Access. Když kliknete na dlaždici CyberSolutions MAILBASEΣ \ CMS na přístupovém panelu, pokud se nakonfiguruje v režimu SP, budete přesměrováni na přihlašovací stránku aplikace pro inicializaci toku přihlášení a pokud je nakonfigurovaná v režimu IDP, měli byste se automaticky přihlásit k CyberSolutions MAILBASEΣ \ CMS, pro který jste nastavili jednotné přihlašování. Další informace o přístupovém panelu najdete v tématu [Úvod do přístupového panelu](../user-help/my-apps-portal-end-user-access.md).

## <a name="next-steps"></a>Další kroky

Po nakonfigurování CyberSolutions MAILBASEΣ \ CMS můžete vynutili řízení relace, které chrání exfiltrace a infiltraci citlivých dat vaší organizace v reálném čase. Řízení relace se rozšiřuje z podmíněného přístupu. [Přečtěte si, jak vynutili řízení relace pomocí Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-any-app).