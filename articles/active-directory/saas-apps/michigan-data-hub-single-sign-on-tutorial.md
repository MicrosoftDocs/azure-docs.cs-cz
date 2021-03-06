---
title: 'Kurz: Azure Active Directory integraci jednotného přihlašování (SSO) s jedním Sign-Onm datového centra Michigan | Microsoft Docs'
description: Přečtěte si, jak nakonfigurovat jednotné přihlašování mezi Azure Active Directory a Michigan a jednotným přihlašováním centra dat.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 07/23/2020
ms.author: jeedes
ms.openlocfilehash: acdfd8b6c57ad2005f116ffb1e5a3c94a5cb87f2
ms.sourcegitcommit: 59f506857abb1ed3328fda34d37800b55159c91d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/24/2020
ms.locfileid: "92522627"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-michigan-data-hub-single-sign-on"></a>Kurz: Azure Active Directory integraci jednotného přihlašování (SSO) s jedním Sign-Onm datového centra Michigan

V tomto kurzu se dozvíte, jak integrovat Michigan data hub Single Sign-On s Azure Active Directory (Azure AD). Když integruje Michigan data hub Single Sign-On s Azure AD, můžete:

* Řízení ve službě Azure AD, která má přístup k jednotnému přihlašování k Michigan data hub.
* Umožněte, aby se vaši uživatelé automaticky přihlásili k Michigan datovému Sign-On centru pomocí svých účtů Azure AD.
* Spravujte svoje účty v jednom centrálním umístění – Azure Portal.

Další informace o integraci aplikací SaaS s Azure AD najdete v tématu [co je přístup k aplikacím a jednotné přihlašování pomocí Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Předpoklady

Chcete-li začít, potřebujete následující položky:

* Předplatné služby Azure AD. Pokud předplatné nemáte, můžete získat [bezplatný účet](https://azure.microsoft.com/free/).
* Michigan data hub Single Sign-On předplatné s povoleným jednotným přihlašováním (SSO).

## <a name="scenario-description"></a>Popis scénáře

V tomto kurzu nakonfigurujete a otestujete jednotné přihlašování Azure AD v testovacím prostředí.

* Michigan data hub Single Sign-On podporuje jednotné přihlašování spouštěné v **SP**
* Jakmile nakonfigurujete jeden Sign-On Michigan data hub, můžete vynutili řízení relace, které chrání exfiltrace a infiltraci citlivých dat vaší organizace v reálném čase. Řízení relace se rozšiřuje z podmíněného přístupu. [Přečtěte si, jak vynutili řízení relace pomocí Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-any-app).

## <a name="adding-michigan-data-hub-single-sign-on-from-the-gallery"></a>Přidání jednoho Sign-On datového centra Michigan z Galerie

Pokud chcete nakonfigurovat integraci Michigan data hub Single Sign-On do služby Azure AD, musíte do seznamu spravovaných aplikací pro SaaS přidat Sign-On datového centra Michigan z galerie.

1. Přihlaste se k [Azure Portal](https://portal.azure.com) pomocí pracovního nebo školního účtu nebo osobního účet Microsoft.
1. V levém navigačním podokně vyberte službu **Azure Active Directory** .
1. Přejděte na **podnikové aplikace** a pak vyberte **všechny aplikace**.
1. Chcete-li přidat novou aplikaci, vyberte možnost **Nová aplikace**.
1. V části **Přidat z Galerie** zadejte do vyhledávacího pole **jednotné přihlašování Michigan data hub** .
1. Na panelu výsledků vyberte **jednotné přihlašování Michigan data hub** a pak aplikaci přidejte. Počkejte několik sekund, než se aplikace přidá do vašeho tenanta.


## <a name="configure-and-test-azure-ad-sso-for-michigan-data-hub-single-sign-on"></a>Konfigurace a testování jednotného přihlašování služby Azure AD pro Michigan data hub na jednom Sign-On

Nakonfigurujte a otestujte jednotné přihlašování Azure AD pomocí Michigan data hub s jedním Sign-On pomocí testovacího uživatele s názvem **B. Simon**. Aby jednotné přihlašování fungovalo, je potřeba vytvořit propojení mezi uživatelem služby Azure AD a souvisejícím uživatelem v rámci jednotného přihlašování Michigan data hub.

Pokud chcete nakonfigurovat a otestovat jednotné přihlašování Azure AD pomocí jednotného přihlašování Michigan data hub, dokončete následující stavební bloky:

1. **[NAKONFIGURUJTE jednotné přihlašování Azure AD](#configure-azure-ad-sso)** – umožníte uživatelům používat tuto funkci.
    1. **[Vytvořte testovacího uživatele Azure AD](#create-an-azure-ad-test-user)** – k otestování jednotného přihlašování Azure AD pomocí B. Simon.
    1. **[Přiřaďte testovacího uživatele Azure AD](#assign-the-azure-ad-test-user)** – Pokud chcete povolit B. Simon používat jednotné přihlašování Azure AD.
1. **[Nakonfigurovat Michigan jednotné PŘIhlašování pro dataSign-On centrum dat](#configure-michigan-data-hub-single-sign-on-sso)** – ke konfiguraci nastavení jednotného přihlašování na straně aplikace
    1. **[Vytvořte Michigan data hub single Sign-On Test User](#create-michigan-data-hub-single-sign-on-test-user)** , abyste měli protějšek B. Simon v Michiganch datových Sign-On rozbočovačích, který je propojený s reprezentací uživatele Azure AD.
1. **[Test SSO](#test-sso)** – ověřte, zda konfigurace funguje.

## <a name="configure-azure-ad-sso"></a>Konfigurace jednotného přihlašování v Azure AD

Pomocí těchto kroků povolíte jednotné přihlašování služby Azure AD v Azure Portal.

1. V [Azure Portal](https://portal.azure.com/)na stránce integrace aplikace **jednotného přihlašování Michigan data hub** najděte část **Správa** a vyberte **jednotné přihlašování**.
1. Na stránce **Vyberte metodu jednotného přihlašování** vyberte **SAML**.
1. Na stránce **nastavit jednotné přihlašování pomocí SAML** klikněte na ikonu Upravit/pero pro **základní konfiguraci SAML** a upravte nastavení.

   ![Upravit základní konfiguraci SAML](common/edit-urls.png)

1. V části **základní konfigurace SAML** zadejte hodnoty pro následující pole:

    Do textového pole **přihlašovací adresa URL** zadejte adresu URL:  `https://launchpad.midatahub.org`

1. Na stránce **nastavit jednotné přihlašování pomocí SAML** v části **podpisový certifikát SAML** kliknutím na tlačítko Kopírovat zkopírujte **adresu URL federačních metadat aplikace** a uložte ji do svého počítače.

    ![Odkaz na stažení certifikátu](common/copy-metadataurl.png)

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

V této části povolíte B. Simon používat jednotné přihlašování pomocí Azure tím, že udělíte přístup k jednotnému přihlašování Michigan data hub.

1. V Azure Portal vyberte **podnikové aplikace**a pak vyberte **všechny aplikace**.
1. V seznamu aplikace vyberte možnost **jednotné přihlašování Michigan data hub**.
1. Na stránce Přehled aplikace najděte část **Správa** a vyberte **Uživatelé a skupiny**.

   ![Odkaz uživatelé a skupiny](common/users-groups-blade.png)

1. Vyberte **Přidat uživatele**a pak v dialogovém okně **Přidat přiřazení** vyberte **Uživatelé a skupiny** .

    ![Odkaz Přidat uživatele](common/add-assign-user.png)

1. V dialogovém okně **Uživatelé a skupiny** vyberte v seznamu uživatelé možnost **B. Simon** a pak klikněte na tlačítko **Vybrat** v dolní části obrazovky.
1. Pokud očekáváte hodnotu role v kontrolním výrazu SAML, v dialogovém okně **Vybrat roli** vyberte v seznamu příslušnou roli pro uživatele a pak klikněte na tlačítko **Vybrat** v dolní části obrazovky.
1. V dialogovém okně **Přidat přiřazení** klikněte na tlačítko **přiřadit** .

## <a name="configure-michigan-data-hub-single-sign-on-sso"></a>Konfigurace Sign-On jednotného přihlašování pro Michigan data hub

Pokud chcete nakonfigurovat jednotné přihlašování na straně **jednotného přihlašování Michigan data hub** , je potřeba odeslat **adresu URL federačních metadat aplikace** do [Michiganho týmu datového centra, který podporuje jeden Sign-On tým podpory](mailto:support@midatahub.org). Toto nastavení nastaví, aby bylo správně nastaveno připojení SAML SSO na obou stranách.

### <a name="create-michigan-data-hub-single-sign-on-test-user"></a>Vytvořit Michigan testovacího uživatele pro jednoho Sign-On datového centra

V této části vytvoříte uživatele s názvem B. Simon v rámci jednotného přihlašování Michigan data hub. Pokud chcete přidat uživatele na Michigan platformu Michigan data hub, pracujte s [Sign-On jedním](mailto:support@midatahub.org) Sign-On platformou datového centra. Před použitím jednotného přihlašování je nutné vytvořit a aktivovat uživatele.

## <a name="test-sso"></a>Test SSO 

V této části otestujete konfiguraci jednotného přihlašování Azure AD pomocí přístupového panelu.

Po kliknutí na dlaždici Michigan data hub Single Sign-On na přístupovém panelu byste měli být automaticky přihlášeni k Michigan datovému Sign-On rozbočovači, pro který jste nastavili jednotné přihlašování. Další informace o přístupovém panelu najdete v tématu [Úvod do přístupového panelu](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Další materiály

- [ Seznam kurzů pro integraci aplikací SaaS s Azure Active Directory ](./tutorial-list.md)

- [Co je přístup k aplikacím a jednotné přihlašování pomocí Azure Active Directory? ](../manage-apps/what-is-single-sign-on.md)

- [Co je podmíněný přístup v Azure Active Directory?](../conditional-access/overview.md)

- [Vyzkoušejte Michigan data hub Single Sign-On s Azure AD](https://aad.portal.azure.com/)

- [Co je řízení relace v Microsoft Cloud App Security?](/cloud-app-security/proxy-intro-aad)

- [Jak chránit Michigan data hub Single Sign-On s pokročilou viditelností a ovládacími prvky](/cloud-app-security/proxy-intro-aad)