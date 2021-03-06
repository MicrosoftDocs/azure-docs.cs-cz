---
title: 'Kurz: konfigurace podnikového spravovaného uživatele GitHubu pro Automatické zřizování uživatelů s Azure Active Directory | Microsoft Docs'
description: Přečtěte si, jak automaticky zřídit a zrušit zřízení uživatelských účtů z Azure AD do GitHubu Enterprise spravovaného uživatele.
services: active-directory
documentationcenter: ''
author: Zhchia
writer: Zhchia
manager: beatrizd
ms.assetid: 6aee39c7-08a1-4110-b936-4c85d129743b
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/05/2021
ms.author: Zhchia
ms.openlocfilehash: 3efb346bc8796c82adb403ad65834cadc6782c09
ms.sourcegitcommit: 5f32f03eeb892bf0d023b23bd709e642d1812696
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/12/2021
ms.locfileid: "103196683"
---
# <a name="tutorial-configure-github-enterprise-managed-user-for-automatic-user-provisioning"></a>Kurz: konfigurace podnikového spravovaného uživatele GitHubu pro Automatické zřizování uživatelů

Tento kurz popisuje kroky, které je třeba provést v rámci uživatele GitHub Enterprise Managed User a Azure Active Directory (Azure AD) ke konfiguraci automatického zřizování uživatelů. Po nakonfigurování Azure AD automaticky zřídí a odzřídí uživatele a skupiny se službou GitHub Enterprise Managed User pomocí služby zřizování Azure AD. Důležité podrobnosti o tom, co tato služba dělá a jak funguje, a odpovědi na nejčastější dotazy najdete v tématu [Automatizace zřizování a rušení zřízení uživatelů pro aplikace SaaS ve službě Azure Active Directory](../manage-apps/user-provisioning.md).


## <a name="capabilities-supported"></a>Podporované funkce
> [!div class="checklist"]
> * Vytvoření uživatelů v GitHub Enterprise Managed User
> * Odebrat uživatele v GitHubu Enterprise spravovaného uživatele, když už nevyžadují přístup
> * Udržování uživatelských atributů synchronizovaných mezi službou Azure AD a podnikovým spravovaným uživatelem GitHubu
> * Zřizování skupin a členství ve skupinách v rámci podnikového spravovaného uživatele GitHubu
> * Jednotné přihlašování k GitHub Enterprise Managed User (doporučeno)

## <a name="prerequisites"></a>Požadavky

Scénář popsaný v tomto kurzu předpokládá, že už máte následující požadavky:

* [Tenant Azure AD](https://docs.microsoft.com/azure/active-directory/develop/quickstart-create-new-tenant)
* Uživatelský účet ve službě Azure AD s [oprávněním](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) ke konfiguraci zřizování (například správce aplikace, správce cloudové aplikace, vlastník aplikace nebo globální správce).
* Podnikoví podnikoví uživatelé mají povolený GitHub Enterprise a nakonfigurovali se na přihlášení pomocí jednotného přihlašování SAML prostřednictvím vašeho tenanta Azure AD.

## <a name="step-1-plan-your-provisioning-deployment"></a>Krok 1. Plánování nasazení zřizování
1. Seznamte se s [fungováním služby zřizování](https://docs.microsoft.com/azure/active-directory/manage-apps/user-provisioning).
2. Zjistěte, kdo bude v [rozsahu zřizování](https://docs.microsoft.com/azure/active-directory/manage-apps/define-conditional-rules-for-provisioning-user-accounts).
3. Určete, jaká data se mají [mapovat mezi Azure AD a podnikovým spravovaným uživatelem GitHubu](https://docs.microsoft.com/azure/active-directory/manage-apps/customize-application-attributes).

## <a name="step-2-configure-github-enterprise-managed-user-to-support-provisioning-with-azure-ad"></a>Krok 2. Konfigurace podnikového spravovaného uživatele GitHubu pro podporu zřizování s Azure AD

1. Adresa URL tenanta je `https://api.github.com/scim/v2/enterprises/{enterprise}` . Tato hodnota se zadá do pole Adresa URL tenanta na kartě zřizování vaší aplikace spravovaného uživatele GitHubu v rámci portálu Azure Portal.

2. Jako podnikový spravovaný správce GitHubu přejděte do pravého horního rohu > klikněte na profil fotografie > pak klikněte na **Nastavení**.

3. V levém bočním panelu klikněte na **nastavení pro vývojáře**.

4. V levém bočním panelu klikněte na **osobní přístupové tokeny**.

5. Klikněte na **vygenerovat nový token**.

6. Vyberte obor **správce: obor organizace** pro tento token.

7. Klikněte na **vygenerovat token**.

8. Zkopírujte a uložte **tajný token**. Tato hodnota se zadá do pole token tajného klíče na kartě zřizování vaší aplikace spravovaného uživatele GitHubu v rámci portálu Azure Portal.

## <a name="step-3-add-github-enterprise-managed-user-from-the-azure-ad-application-gallery"></a>Krok 3. Přidat spravovaného uživatele GitHubu z Galerie aplikací Azure AD

Přidejte spravovaného uživatele GitHub Enterprise z Galerie aplikací Azure AD a začněte spravovat zřizování pro podnikového spravovaného uživatele GitHub. Pokud jste dříve nastavili pro jednotné přihlašování na webu GitHub Enterprise spravovaného uživatele, můžete použít stejnou aplikaci. Pro účely počátečního testování integrace však doporučujeme vytvořit samostatnou aplikaci. Další informace o přidání aplikace z galerie najdete [tady](https://docs.microsoft.com/azure/active-directory/manage-apps/add-gallery-app).

## <a name="step-4-define-who-will-be-in-scope-for-provisioning"></a>Krok 4: Definování uživatelů, kteří budou v rozsahu zřizování

Služba zřizování Azure AD umožňuje nastavit rozsah uživatelů, kteří se zřídí, na základě přiřazení k aplikaci nebo atributů jednotlivých uživatelů nebo skupin. Pokud se rozhodnete nastavit rozsah uživatelů, kteří se zřídí pro vaši aplikaci, na základě přiřazení, můžete k aplikaci přiřadit uživatele a skupiny pomocí následujících [kroků](../manage-apps/assign-user-or-group-access-portal.md). Pokud se rozhodnete nastavit rozsah uživatelů, kteří se zřídí, pouze na základě atributů jednotlivých uživatelů nebo skupin, můžete použít filtr rozsahu, jak je popsáno [tady](https://docs.microsoft.com/azure/active-directory/manage-apps/define-conditional-rules-for-provisioning-user-accounts).

* Při přiřazování uživatelů a skupin ke spravovanému uživateli GitHubu je nutné vybrat jinou roli než **výchozí přístup**. Uživatelé s rolí Výchozí přístup jsou vyloučeni ze zřizování a v protokolech zřizování se označí příznakem neplatného nároku.

* Začněte v malém. Než se pustíte do zavádění pro všechny, proveďte testování s malou skupinou uživatelů a skupin. Pokud je rozsah zřizování nastavený na přiřazené uživatele a skupiny, můžete testování provést tak, že k aplikaci přiřadíte jednoho nebo dva uživatele nebo skupiny. Pokud je rozsah nastavený na všechny uživatele a skupiny, můžete určit [filtr rozsahu na základě atributů](https://docs.microsoft.com/azure/active-directory/manage-apps/define-conditional-rules-for-provisioning-user-accounts).


## <a name="step-5-configure-automatic-user-provisioning-to-github-enterprise-managed-user"></a>Krok 5. Konfigurace automatického zřizování uživatelů na webu GitHub Enterprise Managed User

V této části se seznámíte s postupem konfigurace služby zřizování Azure AD k vytváření, aktualizaci a zakázání uživatelů nebo skupin v TestApp na základě přiřazení uživatelů nebo skupin ve službě Azure AD.

### <a name="to-configure-automatic-user-provisioning-for-github-enterprise-managed-user-in-azure-ad"></a>Konfigurace automatického zřizování uživatelů pro uživatele GitHub Enterprise Managed v Azure AD:

1. Přihlaste se k webu [Azure Portal](https://portal.azure.com). Vyberte **Podnikové aplikace** a pak vyberte **Všechny aplikace**.

    ![Okno Podnikové aplikace](common/enterprise-applications.png)

2. V seznamu aplikace vyberte **GitHub Enterprise Managed User**.

    ![Odkaz na spravovaného uživatele GitHubu v seznamu aplikací](common/all-applications.png)

3. Vyberte kartu **Zřizování**.

    ![Karta Zřizování](common/provisioning.png)

4. Nastavte **Režim zřizování** na hodnotu **Automaticky**.

    ![Automatická karta zřizování](common/provisioning-automatic.png)

5. V části **přihlašovací údaje správce** zadejte adresu URL tenanta spravovaného uživatele GitHubu Enterprise a tajný token. Klikněte na **Test připojení** a ujistěte se, že se služba Azure AD může připojit k webu GitHub Enterprise Managed User. Pokud se připojení nepovede, ujistěte se, že váš účet spravovaného podnikového účtu GitHub vytvořil jako vlastníka podniku token tajného uživatele, a zkuste to znovu.

    ![Token](common/provisioning-testconnection-tenanturltoken.png)

6. Do pole **Oznamovací e-mail** zadejte e-mailovou adresu osoby nebo skupiny, na kterou by se měla odesílat oznámení o chybách zřizování, a zaškrtněte políčko **Když dojde k selhání, poslat oznámení e-mailem**.

    ![Oznamovací e-mail](common/provisioning-notification-email.png)

7. Vyberte **Uložit**.

8. V části **mapování** vyberte **synchronizovat Azure Active Directory uživatelů na GitHub Enterprise Managed User**.

9. Zkontrolujte atributy uživatele, které se synchronizují z Azure AD do webu GitHub Enterprise Managed User v oddílu **mapování atributů** . Atributy vybrané jako **odpovídající** vlastnosti se používají ke spárování uživatelských účtů na webu GitHub Enterprise Managed User pro operace aktualizace. Pokud se rozhodnete změnit [odpovídající cílový atribut](https://docs.microsoft.com/azure/active-directory/manage-apps/customize-application-attributes), budete muset zajistit, že rozhraní API spravovaného uživatele GitHubu podporuje filtrování uživatelů na základě tohoto atributu. Kliknutím na tlačítko **Uložit** potvrďte změny.

   |Atribut|Typ|Podporováno pro filtrování|
   |---|---|---|
   |externalId|Řetězec|&check;|
   |userName|Řetězec|
   |active|Logická hodnota|
   |Role|Řetězec|
   |displayName|Řetězec|
   |name.givenName|Řetězec|
   |name.familyName|Řetězec|
   |název. formátovaný|Řetězec|
   |emails[type eq "work"].value|Řetězec|
   |e-maily [typ EQ "domů"]. hodnota|Řetězec|
   |e-maily [typ EQ "other"]. hodnota|Řetězec|

10. V části **mapování** vyberte možnost **synchronizovat Azure Active Directory skupiny se spravovaným uživatelem GitHub Enterprise**.

11. Zkontrolujte atributy skupiny, které se synchronizují z Azure AD do GitHub Enterprise Managed User v oddílu **mapování atributů** . Atributy vybrané jako **odpovídající** vlastnosti se používají ke spárování skupin v rámci podnikového spravovaného uživatele GitHubu pro operace aktualizace. Kliknutím na tlačítko **Uložit** potvrďte změny.

      |Atribut|Typ|Podporováno pro filtrování|
      |---|---|---|
      |externalId|Řetězec|&check;|
      |displayName|Řetězec|
      |členy|Referenční informace|

12. Pokud chcete nakonfigurovat filtry rozsahu, postupujte podle pokynů uvedených v [kurzu k filtrům rozsahu](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).

13. Pokud chcete povolit službu zřizování Azure AD pro spravovaného uživatele GitHubu, změňte **stav zřizování** na **zapnuto** v části **Nastavení** .

    ![Zapnutý přepínač Stav zřizování](common/provisioning-toggle-on.png)

14. Definujte uživatele nebo skupiny, které chcete zřídit pro podnikového spravovaného uživatele GitHubu, a to tak, že v části **Nastavení** vyberete požadované hodnoty v poli **Rozsah** .

    ![Rozsah zřizování](common/provisioning-scope.png)

15. Jakmile budete připraveni na zřízení, klikněte na **Uložit**.

    ![Uložení konfigurace zřizování](common/provisioning-configuration-save.png)

Tato operace zahájí cyklus počáteční synchronizace všech uživatelů a skupin definovaných v nabídce **Rozsah** v části **Nastavení**. Počáteční cyklus trvá déle než další cykly, které se provádějí přibližně každých 40 minut, pokud je služba zřizování Azure AD spuštěná.

## <a name="step-6-monitor-your-deployment"></a>Krok 6. Monitorování nasazení
Po dokončení konfigurace zřizování můžete své nasazení monitorovat pomocí následujících prostředků:

1. S využitím [protokolů zřizování](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-provisioning-logs) můžete zjistit, kteří uživatelé se zřídili úspěšně a kteří neúspěšně.
2. Pokud chcete zjistit, jaký je stav cyklu zřizování a jak blízko je dokončení, zkontrolujte [indikátor průběhu](https://docs.microsoft.com/azure/active-directory/app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user).
3. Pokud se zdá, že konfigurace zřizování není v pořádku, aplikace přejde do karantény. Další informace o stavech karantény najdete [tady](https://docs.microsoft.com/azure/active-directory/manage-apps/application-provisioning-quarantine-status).

## <a name="additional-resources"></a>Další zdroje informací

* [Správa zřizování uživatelských účtů pro podnikové aplikace](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [Jak ve službě Azure Active Directory probíhá přístup k aplikacím a jednotné přihlašování?](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a>Další kroky

* [Zjistěte, jak procházet protokoly a získat sestavy aktivit zřizování](../manage-apps/check-status-user-account-provisioning.md).
