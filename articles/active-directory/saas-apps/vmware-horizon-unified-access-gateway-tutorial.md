---
title: 'Kurz: Azure Active Directory integrace jednotného přihlašování s využitím VMware Horizon – Unified Access Gateway | Microsoft Docs'
description: Přečtěte si, jak nakonfigurovat jednotné přihlašování mezi Azure Active Directory a VMware Horizon – brána Unified Access.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 02/04/2021
ms.author: jeedes
ms.openlocfilehash: cf1e71d67424258ccae6794f28d37399cd68996e
ms.sourcegitcommit: b4647f06c0953435af3cb24baaf6d15a5a761a9c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2021
ms.locfileid: "101654319"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-vmware-horizon---unified-access-gateway"></a>Kurz: Azure Active Directory integrace jednotného přihlašování s využitím VMware Horizon – Unified Access Gateway

V tomto kurzu se dozvíte, jak integrovat službu VMware Horizon – Unified Access Gateway s Azure Active Directory (Azure AD). Když integrujete službu VMware Horizon – Unified Access Gateway s Azure AD, můžete:

* Řízení ve službě Azure AD, která má přístup k bráně VMware Horizon – Unified Access Gateway.
* Umožněte uživatelům, aby se automaticky přihlásili k bráně VMware Horizon – Unified Access Gateway s účty Azure AD.
* Spravujte svoje účty v jednom centrálním umístění – Azure Portal.

## <a name="prerequisites"></a>Požadavky

Chcete-li začít, potřebujete následující položky:

* Předplatné služby Azure AD. Pokud předplatné nemáte, můžete získat [bezplatný účet](https://azure.microsoft.com/free/).
* VMware Horizon – Unified Access Gateway s povoleným jednotným přihlašováním (SSO).

## <a name="scenario-description"></a>Popis scénáře

V tomto kurzu nakonfigurujete a otestujete jednotné přihlašování Azure AD v testovacím prostředí.

* VMware Horizon – brána Unified Accessu podporuje **aktualizace SP a IDP, které** iniciovaly jednotné přihlašování

## <a name="add-vmware-horizon---unified-access-gateway-from-the-gallery"></a>Přidání brány VMware Horizon – Unified Access Gateway z Galerie

Pokud chcete nakonfigurovat integraci VMware Horizon-Unified Access Gateway do služby Azure AD, musíte do seznamu spravovaných aplikací SaaS přidat bránu VMware Horizon – Unified Access Gateway z galerie.

1. Přihlaste se k Azure Portal pomocí pracovního nebo školního účtu nebo osobního účet Microsoft.
1. V levém navigačním podokně vyberte službu **Azure Active Directory** .
1. Přejděte na **podnikové aplikace** a pak vyberte **všechny aplikace**.
1. Chcete-li přidat novou aplikaci, vyberte možnost **Nová aplikace**.
1. V části **Přidat z Galerie** do vyhledávacího pole zadejte **VMware Horizon – Unified Access Gateway** .
1. Vyberte **VMware Horizon – Unified Access Gateway** z panelu výsledků a pak přidejte aplikaci. Počkejte několik sekund, než se aplikace přidá do vašeho tenanta.


## <a name="configure-and-test-azure-ad-sso-for-vmware-horizon---unified-access-gateway"></a>Konfigurace a testování jednotného přihlašování služby Azure AD pro VMware Horizon – Unified Access Gateway

Konfigurace a testování jednotného přihlašování služby Azure AD pomocí VMware Horizon – Unified Access Gateway s použitím testovacího uživatele s názvem **B. Simon**. Aby jednotné přihlašování fungovalo, musíte vytvořit vztah propojení mezi uživatelem služby Azure AD a souvisejícím uživatelem v bráně VMware Horizon – Unified Access Gateway.

Pokud chcete nakonfigurovat a otestovat jednotné přihlašování Azure AD pomocí nástroje VMware Horizon – Unified Access Gateway, proveďte následující kroky:

1. **[NAKONFIGURUJTE jednotné přihlašování Azure AD](#configure-azure-ad-sso)** – umožníte uživatelům používat tuto funkci.
    1. **[Vytvořte testovacího uživatele Azure AD](#create-an-azure-ad-test-user)** – k otestování jednotného přihlašování Azure AD pomocí B. Simon.
    1. **[Přiřaďte testovacího uživatele Azure AD](#assign-the-azure-ad-test-user)** – Pokud chcete povolit B. Simon používat jednotné přihlašování Azure AD.
1. **[NAKONFIGURUJTE jednotné přihlašování VMware Horizon-Unified Access Gateway](#configure-vmware-horizon-unified-access-gateway-sso)** – ke konfiguraci nastavení jednotného přihlašování na straně aplikace.
    1. **[Vytvoření testovacího uživatele brány vmware Horizon-Unified Access Gateway](#create-vmware-horizon-unified-access-gateway-test-user)** – Pokud chcete mít protějšek B. Simon ve VMware horizont-Unified Access Gateway, která je propojená s reprezentací uživatele v Azure AD.
1. **[Test SSO](#test-sso)** – ověřte, zda konfigurace funguje.

## <a name="configure-azure-ad-sso"></a>Konfigurace jednotného přihlašování v Azure AD

Pomocí těchto kroků povolíte jednotné přihlašování služby Azure AD v Azure Portal.

1. V Azure Portal na stránce integrace **VMware Horizon – Unified Access Gateway** najděte část **Správa** a vyberte **jednotné přihlašování**.
1. Na stránce **Vyberte metodu jednotného přihlašování** vyberte **SAML**.
1. Na stránce **nastavit jednotné přihlašování pomocí SAML** klikněte na ikonu tužky pro **základní konfiguraci SAML** a upravte nastavení.

   ![Upravit základní konfiguraci SAML](common/edit-urls.png)

1. Pokud chcete nakonfigurovat aplikaci v režimu iniciované **IDP** , zadejte v **základní části Konfigurace SAML** hodnoty následujících polí:

    a. Do textového pole **identifikátor** zadejte adresu URL pomocí následujícího vzoru: `https://<HORIZON_UAG_FQDN>/portal`

    b. Do textového pole **Adresa URL odpovědi** zadejte adresu URL pomocí následujícího vzoru: `https://<HORIZON_UAG_FQDN>/portal/samlsso`

1. Klikněte na **nastavit další adresy URL** a proveďte následující krok, pokud chcete nakonfigurovat aplikaci v režimu iniciované **SP** :

    Do textového pole **přihlašovací adresa URL** zadejte adresu URL pomocí následujícího vzoru:  `https://<HORIZON_UAG_FQDN>`

    > [!NOTE]
    > Tyto hodnoty nejsou reálné. Aktualizujte tyto hodnoty skutečným identifikátorem, adresou URL odpovědi a přihlašovací adresou URL. Obraťte se na [tým podpory pro službu VMware Horizon – Unified Access Gateway](mailto:support@vmware.com) , který tyto hodnoty získá. Můžete se také podívat na vzory uvedené v části **základní konfigurace SAML** v Azure Portal.

1. Na stránce **nastavit jednotné přihlašování pomocí SAML** v části **podpisový certifikát SAML** Najděte **XML metadata federace** a vyberte **Stáhnout** a Stáhněte certifikát a uložte ho do svého počítače.

    ![Odkaz na stažení certifikátu](common/metadataxml.png)

1. V části **Nastavení VMware Horizon – Unified Access Gateway** zkopírujte příslušné adresy URL na základě vašeho požadavku.

    ![Kopírovat adresy URL konfigurace](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Vytvoření testovacího uživatele Azure AD

V této části vytvoříte testovacího uživatele ve Azure Portal s názvem B. Simon.

1. V levém podokně Azure Portal vyberte možnost **Azure Active Directory**, vyberte možnost **Uživatelé** a potom vyberte možnost **Všichni uživatelé**.
1. V horní části obrazovky vyberte **Nový uživatel** .
1. Ve vlastnostech **uživatele** proveďte následující kroky:
   1. Do pole **Název** zadejte `B.Simon`.  
   1. Do pole **uživatelské jméno** zadejte username@companydomain.extension . Například, `B.Simon@contoso.com`.
   1. Zaškrtněte políčko **Zobrazit heslo** a pak zapište hodnotu, která se zobrazí v poli **heslo** .
   1. Klikněte na **Vytvořit**.

### <a name="assign-the-azure-ad-test-user"></a>Přiřazení testovacího uživatele Azure AD

V této části povolíte B. Simon používat jednotné přihlašování pomocí Azure tím, že udělíte přístup k bráně VMware Horizon – Unified Access Gateway.

1. V Azure Portal vyberte **podnikové aplikace** a pak vyberte **všechny aplikace**.
1. V seznamu aplikace vyberte **VMware Horizon – Unified Access Gateway**.
1. Na stránce Přehled aplikace najděte část **Správa** a vyberte **Uživatelé a skupiny**.
1. Vyberte **Přidat uživatele** a pak v dialogovém okně **Přidat přiřazení** vyberte **Uživatelé a skupiny** .
1. V dialogovém okně **Uživatelé a skupiny** vyberte v seznamu uživatelé možnost **B. Simon** a pak klikněte na tlačítko **Vybrat** v dolní části obrazovky.
1. Pokud očekáváte, že role má být přiřazena uživatelům, můžete ji vybrat v rozevíracím seznamu **Vybrat roli** . Pokud pro tuto aplikaci nebyla nastavena žádná role, zobrazí se vybraná role výchozí přístup.
1. V dialogovém okně **Přidat přiřazení** klikněte na tlačítko **přiřadit** .

## <a name="configure-vmware-horizon-unified-access-gateway-sso"></a>Konfigurace jednotného přihlašování k VMware Horizon-Unified Access Gateway

Pokud chcete nakonfigurovat jednotné přihlašování na straně **brány VMware Horizon (Unified Access Gateway** ), musíte stáhnout stažená **metadata federačních metadat** a příslušné zkopírované adresy URL z Azure Portal do [týmu podpory VMware Horizon – Unified Access Gateway](mailto:support@vmware.com). Toto nastavení nastaví, aby bylo správně nastaveno připojení SAML SSO na obou stranách.

### <a name="create-vmware-horizon-unified-access-gateway-test-user"></a>Vytvořit testovacího uživatele brány VMware Horizon-Unified Access

V této části vytvoříte uživatele s názvem B. Simon v bráně VMware Horizon – Unified Access Gateway. Pokud chcete přidat uživatele na platformě VMware Horizon – Unified Access Gateway, pracujte s [týmem podpory VMware Horizon – Unified Access](mailto:support@vmware.com) Gateway. Před použitím jednotného přihlašování je nutné vytvořit a aktivovat uživatele.

## <a name="test-sso"></a>Test SSO 

V této části otestujete konfiguraci jednotného přihlašování Azure AD pomocí následujících možností. 

#### <a name="sp-initiated"></a>Zahájena SP:

* Kliknutím na **test této aplikace** v Azure Portal. Tím se přesměruje na přihlašovací adresu URL VMware Horizon – Unified Access Gateway, kde můžete spustit tok přihlášení.  

* Přejít na adresu URL služby VMware Horizon – Unified Access Gateway přímo a spustit tok přihlášení z tohoto účtu.

#### <a name="idp-initiated"></a>Iniciované IDP:

* Klikněte na **testovat tuto aplikaci** v Azure Portal a měli byste se automaticky přihlášeni k bráně VMware Horizon – Unified Access Gateway, pro kterou jste si nastavili jednotné přihlašování. 

K otestování aplikace v jakémkoli režimu můžete také použít panel Microsoft Access. Po kliknutí na dlaždici VMware Horizon – Unified Access Gateway na přístupovém panelu byste se měli automaticky přihlášeni k bráně VMware Horizon – Unified Access Gateway, pro kterou jste nastavili jednotné přihlašování. Další informace o přístupovém panelu najdete v tématu [Úvod do přístupového panelu](../user-help/my-apps-portal-end-user-access.md).

## <a name="next-steps"></a>Další kroky

Jakmile nakonfigurujete bránu VMware pro sjednocení přístupu, můžete vynutili řízení relace, které chrání exfiltrace a infiltraci citlivých dat vaší organizace v reálném čase. Řízení relace se rozšiřuje z podmíněného přístupu. [Přečtěte si, jak vynutili řízení relace pomocí Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/proxy-deployment-any-app).