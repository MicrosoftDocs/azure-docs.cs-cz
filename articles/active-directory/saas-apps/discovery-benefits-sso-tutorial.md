---
title: 'Kurz: Azure Active Directory integrace jednotného přihlašování s výhodami zjišťování – jednotné přihlašování | Microsoft Docs'
description: Přečtěte si, jak nakonfigurovat jednotné přihlašování mezi Azure Active Directory a PŘIHLÁŠENÍm k výhodám zjišťování.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 10/03/2019
ms.author: jeedes
ms.openlocfilehash: 0e5d67e00ee56b5c4006a8422c713e3cabb32bfc
ms.sourcegitcommit: 9b8425300745ffe8d9b7fbe3c04199550d30e003
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/23/2020
ms.locfileid: "92454758"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-discovery-benefits-sso"></a>Kurz: Azure Active Directory integraci jednotného přihlašování s výhodami zjišťování pro jednotné přihlašování

V tomto kurzu se dozvíte, jak integrovat výhody zjišťování jednotného přihlašování s Azure Active Directory (Azure AD). Když integrujete jednotné přihlašování výhod zjišťování s Azure AD, můžete:

* Řízení ve službě Azure AD, která má přístup k výhodám zjišťování jednotného přihlašování.
* Umožněte, aby se vaši uživatelé automaticky přihlásili k vašemu účtu služby Azure AD ke zjišťování výhod přihlášení.
* Spravujte svoje účty v jednom centrálním umístění – Azure Portal.

Další informace o integraci aplikací SaaS s Azure AD najdete v tématu [co je přístup k aplikacím a jednotné přihlašování pomocí Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Požadavky

Chcete-li začít, potřebujete následující položky:

* Předplatné služby Azure AD. Pokud předplatné nemáte, můžete získat [bezplatný účet](https://azure.microsoft.com/free/).
* Výhody zjišťování: jednotné přihlašování s povoleným jednotným přihlašováním (SSO).

## <a name="scenario-description"></a>Popis scénáře

V tomto kurzu nakonfigurujete a otestujete jednotné přihlašování Azure AD v testovacím prostředí.

* Výhody zjišťování jednotného přihlašování podporuje **IDP** .

> [!NOTE]
> Identifikátorem této aplikace je pevná řetězcová hodnota, takže v jednom tenantovi může být nakonfigurovaná jenom jedna instance.

## <a name="adding-discovery-benefits-sso-from-the-gallery"></a>Přidávají se výhody zjišťování jednotného přihlašování z galerie.

Pokud chcete nakonfigurovat integraci výhod zjišťování jednotného přihlašování do služby Azure AD, musíte do seznamu spravovaných aplikací SaaS přidat výhody zjišťování jednotného přihlašování z galerie.

1. Přihlaste se k [Azure Portal](https://portal.azure.com) pomocí pracovního nebo školního účtu nebo osobního účet Microsoft.
1. V levém navigačním podokně vyberte službu **Azure Active Directory** .
1. Přejděte na **podnikové aplikace** a pak vyberte **všechny aplikace**.
1. Chcete-li přidat novou aplikaci, vyberte možnost **Nová aplikace**.
1. V části **Přidat z Galerie** zadejte do vyhledávacího pole **jednotné přihlašování k výhodám zjišťování** .
1. Vyberte možnost **zjišťování přihlašování** z panelu výsledků a pak přidejte aplikaci. Počkejte několik sekund, než se aplikace přidá do vašeho tenanta.

## <a name="configure-and-test-azure-ad-single-sign-on-for-discovery-benefits-sso"></a>Konfigurace a testování jednotného přihlašování Azure AD pro jednotné přihlašování k výhodám zjišťování

Nakonfigurujte a otestujte jednotné přihlašování Azure AD s výhodami zjišťování jednotného přihlašování pomocí testovacího uživatele s názvem **B. Simon**. Aby jednotné přihlašování fungovalo, je potřeba vytvořit propojení mezi uživatelem služby Azure AD a souvisejícím uživatelem v rámci jednotného přihlašování k výhodám zjišťování.

Pokud chcete nakonfigurovat a otestovat jednotné přihlašování Azure AD pomocí jednotného přihlašování výhod zjišťování, dokončete následující stavební bloky:

1. **[NAKONFIGURUJTE jednotné přihlašování Azure AD](#configure-azure-ad-sso)** – umožníte uživatelům používat tuto funkci.
    1. **[Vytvořte testovacího uživatele Azure AD](#create-an-azure-ad-test-user)** – k otestování jednotného přihlašování Azure AD pomocí B. Simon.
    1. **[Přiřaďte testovacího uživatele Azure AD](#assign-the-azure-ad-test-user)** – Pokud chcete povolit B. Simon používat jednotné přihlašování Azure AD.
1. **[Nakonfigurujte výhody zjišťování](#configure-discovery-benefits-sso-sso)** jednotného přihlašování SSO – ke konfiguraci nastavení jednotného přihlašování na straně aplikace.
    1. **[Vytvořit výhody zjišťování jednotného přihlašování – uživatel](#create-discovery-benefits-sso-test-user)** , který má protějšek B. Simon v přihlašování k výhodám Azure AD, které je propojené s reprezentací uživatele v Azure AD.
1. **[Test SSO](#test-sso)** – ověřte, zda konfigurace funguje.

## <a name="configure-azure-ad-sso"></a>Konfigurace jednotného přihlašování v Azure AD

Pomocí těchto kroků povolíte jednotné přihlašování služby Azure AD v Azure Portal.

1. V [Azure Portal](https://portal.azure.com/)na stránce s integrací aplikace **jednotného přihlašování k výhodám vyhledávání** najděte část **Správa** a vyberte **jednotné přihlašování**.
1. Na stránce **Vyberte metodu jednotného přihlašování** vyberte **SAML**.
1. Na stránce **nastavit jednotné přihlašování pomocí SAML** klikněte na ikonu Upravit/pero pro **základní konfiguraci SAML** a upravte nastavení.

   ![Upravit základní konfiguraci SAML](common/edit-urls.png)

1. V **základním oddílu konfigurace SAML** je aplikace předem nakonfigurovaná v režimu iniciované **IDP** a nezbytné adresy URL už jsou předem naplněné pomocí Azure. Uživatel musí konfiguraci uložit kliknutím na tlačítko **Uložit** .

1. Aplikace jednotného přihlašování pro jednotné přihlašování očekává kontrolní výrazy SAML v určitém formátu, což vyžaduje přidání mapování vlastních atributů do konfigurace atributů tokenu SAML. Následující snímek obrazovky ukazuje seznam výchozích atributů. Kliknutím na tlačítko **Upravit** ikonu otevřete dialogové okno atributy uživatele.

    ![image](common/edit-attribute.png)

    a. Kliknutím na ikonu **Upravit**  otevřete dialogové okno **jedinečný identifikátor uživatele (ID názvu)** .

    ![Snímek obrazovky se sekcí "atributy uživatele & deklaracemi" se třemi tečkami "požadovaná deklarace" na pravé straně.](./media/discovery-benefits-sso-tutorial/attribute01.png)

    ![Konfigurace jednotného přihlašování k výhodám zjišťování](./media/discovery-benefits-sso-tutorial/attribute02.png)

    b. Kliknutím na ikonu **Upravit** otevřete dialogové okno **Spravovat transformaci** .

    c. Do textového pole **transformace** zadejte **ToUppercase ()** zobrazený pro tento řádek.

    d. Do textového pole **parametr 1** zadejte parametr jako `<Name Identifier value>` .

    e. Klikněte na **Přidat**.

    > [!NOTE]
    > K tomu, aby tato integrace fungovala, musí být v poli **jedinečného uživatelského identifikátoru (ID)** předána pevná řetězcová hodnota pro zjišťování výhod. Azure AD v tuto chvíli nepodporuje tuto funkci, takže pokud chcete nastavit pevnou hodnotu řetězce, jak je znázorněno na snímku obrazovky, můžete použít transformace **ToUpper** nebo **ToLower** NameId.

    f. Vyplnili jsme automaticky dodatečné deklarace identity, které jsou potřeba pro konfiguraci jednotného přihlašování ( `SSOInstance` a `SSOID` ). Pomocí ikony **Upravit** namapujte hodnoty dle vaší organizace.

    ![Snímek obrazovky, který zobrazuje "atributy uživatele & deklarace identity" s zvýrazněnými hodnotami "S/O instance" a "S S O D".](./media/discovery-benefits-sso-tutorial/attribute03.png)

1. Na stránce **nastavit jednotné přihlašování pomocí SAML** v části **podpisový certifikát SAML** vyhledejte **certifikát (Base64)** a vyberte **Stáhnout** a Stáhněte certifikát a uložte ho do počítače.

    ![Odkaz na stažení certifikátu](common/certificatebase64.png)

1. V části **nastavení jednotného přihlašování k výhodám zjišťování** zkopírujte příslušné adresy URL na základě vašeho požadavku.

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

V této části povolíte B. Simon používat jednotné přihlašování pomocí Azure tím, že udělíte přístup k výhodám zjišťování jednotného přihlašování.

1. V Azure Portal vyberte **podnikové aplikace**a pak vyberte **všechny aplikace**.
1. V seznamu aplikace vyberte možnost **zjišťování výhody pro jednotné přihlašování**.
1. Na stránce Přehled aplikace najděte část **Správa** a vyberte **Uživatelé a skupiny**.

   ![Odkaz uživatelé a skupiny](common/users-groups-blade.png)

1. Vyberte **Přidat uživatele**a pak v dialogovém okně **Přidat přiřazení** vyberte **Uživatelé a skupiny** .

    ![Odkaz Přidat uživatele](common/add-assign-user.png)

1. V dialogovém okně **Uživatelé a skupiny** vyberte v seznamu uživatelé možnost **B. Simon** a pak klikněte na tlačítko **Vybrat** v dolní části obrazovky.
1. Pokud očekáváte hodnotu role v kontrolním výrazu SAML, v dialogovém okně **Vybrat roli** vyberte v seznamu příslušnou roli pro uživatele a pak klikněte na tlačítko **Vybrat** v dolní části obrazovky.
1. V dialogovém okně **Přidat přiřazení** klikněte na tlačítko **přiřadit** .

## <a name="configure-discovery-benefits-sso-sso"></a>Konfigurovat výhody zjišťování jednotného přihlašování SSO

Chcete-li nakonfigurovat jednotné přihlašování na straně **jednotného přihlašování k výhodám zjišťování** , je třeba odeslat stažený **certifikát (Base64)** a příslušné zkopírované adresy URL z Azure Portal na [tým podpory jednotného přihlašování pro výhody zjišťování](mailto:Jsimpson@DiscoveryBenefits.com). Toto nastavení nastaví, aby bylo správně nastaveno připojení SAML SSO na obou stranách.

### <a name="create-discovery-benefits-sso-test-user"></a>Vytvořit uživatele testu jednotného přihlašování pro uživatele

V této části vytvoříte v rámci jednotného přihlašování k výhodám zjišťování uživatele s názvem Britta Simon. Pokud chcete přidat uživatele na platformě jednotného přihlašování k výhodám zjišťování, využijte [tým podpory pro jednotné přihlašování s výhodami zjišťování](mailto:Jsimpson@DiscoveryBenefits.com) . Před použitím jednotného přihlašování je nutné vytvořit a aktivovat uživatele.

## <a name="test-sso"></a>Test SSO 

V této části otestujete konfiguraci jednotného přihlašování Azure AD pomocí přístupového panelu.

Když na přístupovém panelu kliknete na dlaždici přihlášení k výhodám vyhledávání, měli byste být automaticky přihlášení k výhodám zjišťování, pro které jste nastavili jednotné přihlašování. Další informace o přístupovém panelu najdete v tématu [Úvod do přístupového panelu](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Další zdroje

- [ Seznam kurzů pro integraci aplikací SaaS s Azure Active Directory ](./tutorial-list.md)

- [Co je přístup k aplikacím a jednotné přihlašování pomocí Azure Active Directory? ](../manage-apps/what-is-single-sign-on.md)

- [Co je podmíněný přístup v Azure Active Directory?](../conditional-access/overview.md)

- [Vyzkoušejte si jednotné přihlašování pomocí služby Azure AD](https://aad.portal.azure.com/)