---
title: Zabezpečení instančních objektů ve službě Azure Active Directory
description: Hledání, vyhodnocení a zabezpečení instančních objektů.
services: active-directory
author: BarbaraSelden
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.subservice: fundamentals
ms.topic: conceptual
ms.date: 2/15/2021
ms.author: baselden
ms.reviewer: ajburnle
ms.custom: it-pro, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f92625131a35dc91c860923ec6523c189830f65
ms.sourcegitcommit: 7edadd4bf8f354abca0b253b3af98836212edd93
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/10/2021
ms.locfileid: "102552146"
---
# <a name="securing-service-principals"></a>Zabezpečení instančních objektů

[Instanční objekt služby](https://docs.microsoft.com/azure/active-directory/develop/app-objects-and-service-principals) Azure Active Directory (Azure AD) je místní reprezentace objektu aplikace v jednom tenantovi nebo adresáři.  Funguje jako identita instance aplikace. Instanční objekty definují, kdo má přístup k aplikaci a k jakým prostředkům může aplikace přistupovat. Instanční objekt se vytvoří v každém tenantovi, kde se aplikace používá, a odkazuje na globálně jedinečný objekt aplikace. Tenant zabezpečuje přihlašování a přístup k prostředkům objektu služby.  

### <a name="tenant-service-principal-relationships"></a>Vztahy instančního objektu klienta
Jedna aplikace tenanta má v domovském tenantovi pouze jeden instanční objekt. Webová aplikace nebo rozhraní API pro více tenantů vyžadují instanční objekt v každém tenantovi. Instanční objekt se vytvoří, když uživatel z tohoto tenanta souhlasí s používáním aplikace nebo rozhraní API. Tento souhlas vytvoří vztah 1: n mezi aplikací víceklientské aplikace a přidruženými instančními objekty služby.

Víceklientská aplikace je umístěná v jednom tenantovi a je navržená tak, aby měla instance v jiných klientech. Většina aplikací typu software jako služba (SaaS) je navržená pro více tenantů. Pomocí instančních objektů zajistěte správné stav zabezpečení pro aplikaci a její uživatele v případech použití jediného tenanta i více tenantů.

## <a name="applicationid-and-objectid"></a>ApplicationID a ObjectID

Daná instance aplikace má dvě odlišné vlastnosti: ApplicationID (označuje se také jako ClientID) a ObjectID.

> [!NOTE] 
> Může se stát, že se výrazy aplikace a instančního objektu používají zaměnitelné, pokud se volně odkazuje na aplikaci v kontextu úloh souvisejících s ověřováním. Existují však dvě různé reprezentace aplikací v Azure AD.
 

ApplicationID představuje globální aplikaci a je stejná pro všechny instance aplikace napříč klienty. ObjectID je jedinečná hodnota pro objekt aplikace a představuje instanční objekt. Stejně jako u uživatelů, skupin a dalších prostředků identifikátor ObjectID Pomáhá jednoznačně identifikovat instanci aplikace ve službě Azure AD.

Podrobnější informace o tomto tématu najdete v tématu [vztah aplikace a instančního objektu](https://docs.microsoft.com/azure/active-directory/develop/app-objects-and-service-principals).

Můžete také vytvořit aplikaci a její instanční objekt (ObjectID) v tenantovi pomocí Azure PowerShell, Azure CLI, Microsoft Graph, Azure Portal a dalších nástrojů. 

![Snímek obrazovky znázorňující registraci nové aplikace s zvýrazněnými poli ID aplikace a ID objektu.](./media/securing-service-accounts/secure-principal-image-1.png)

## <a name="service-principal-authentication"></a>Ověřování instančních objektů

Existují dva mechanismy ověřování pomocí instančních objektů – klientské certifikáty a tajné klíče klienta. 

![ Snímek obrazovky s novou stránkou aplikace zobrazující zvýrazněné oblasti certifikáty a tajné klíče klienta.](./media/securing-service-accounts/secure-principal-certificates.png)

Certifikáty jsou bezpečnější: Pokud je to možné, používejte klientské certifikáty. Na rozdíl od klientských tajných klíčů nelze klientské certifikáty omylem vkládat do kódu. Pokud je to možné, používejte Azure Key Vault pro správu certifikátů a tajných kódů, abyste mohli šifrovat následující prostředky pomocí klíčů chráněných moduly hardwarového zabezpečení:

* ověřovací klíče

* klíče účtu úložiště

* šifrovací klíče dat

* soubory. pfx

* hesel 

Další informace o Azure Key Vault a o tom, jak se dá použít pro správu certifikátů a tajných kódů, najdete v tématu [o Azure Key Vault](https://docs.microsoft.com/azure/key-vault/general/overview) a [přiřazení zásad Key Vault přístupu pomocí Azure Portal](https://docs.microsoft.com/azure/key-vault/general/assign-access-policy-portal). 

 ### <a name="challenges-and-mitigations"></a>Výzvy a zmírnění rizik
V následující tabulce jsou uvedeny zmírnění potíží s problémy, se kterými se můžete setkat při používání instančních objektů.


| Výzvy| Omezení rizik |
| - | - |
| Kontroly přístupu pro instanční objekty přiřazené k privilegovaným rolím| Tato funkce je ve verzi Preview a ještě není široce dostupná. |
| Kontroluje přístup instančních objektů.| Ruční kontrola seznamu řízení přístupu prostředku pomocí Azure Portal |
| Nad oprávněnými instančními objekty| Při vytváření účtů služby Automation nebo instančních objektů poskytněte pouze oprávnění, která jsou vyžadována pro daný úkol. Vyhodnoťte existující instanční objekty a zjistěte, jestli můžete snížit oprávnění. |
|Identifikace úprav pověření nebo metod ověřování instančních objektů |Použijte sešit sestav citlivých operací, který může přispět k zmírnění tohoto problému. [Podívejte se na vysvětlení v tomto blogovém příspěvku](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/azure-ad-workbook-to-help-you-assess-solorigate-risk/ba-p/2010718).|

## <a name="find-accounts-using-service-principals"></a>Najít účty pomocí instančních objektů
Spusťte následující příkazy pro vyhledání účtů pomocí instančních objektů.

Použití Azure CLI


`az ad sp list`

Pomocí prostředí PowerShell

`Get-AzureADServicePrincipal -All:$true` 


Další informace najdete v tématu [Get-AzureADServicePrincipal](https://docs.microsoft.com/powershell/module/azuread/get-azureadserviceprincipal) .

## <a name="assess-service-principal-security"></a>Posouzení zabezpečení instančního objektu

Pokud chcete posoudit zabezpečení instančních objektů, ujistěte se, že jste vyhodnotili oprávnění a úložiště přihlašovacích údajů.

Zmírnění potenciálních problémů pomocí následujících informací.
|Výzvy | Omezení rizik|
| - | - |
| Zjištění uživatele, který souhlasí s aplikací pro více tenantů, a zjišťování neoprávněných souhlasu pro víceklientské aplikace | Pokud chcete najít víceklientské aplikace, spusťte následující PowerShell.<br>`Get-AzureADServicePrincipal -All:$true ? {$_.Tags -eq WindowsAzureActiveDirectoryIntegratedApp"}`<br>Zakáže souhlas uživatele. <br>Povolení souhlasu uživatele od ověřených vydavatelů pro vybraná oprávnění (doporučeno) <br> Pomocí podmíněného přístupu můžete zablokovat instanční objekty z nedůvěryhodných umístění. Nakonfigurujte je v kontextu uživatele a jejich tokeny by se měly používat k aktivaci instančního objektu.|
|Použití pevně zakódovaného tajného klíče ve skriptu pomocí instančního objektu.|Použijte certifikát nebo Azure Key Vault.|
|Sledování, kdo používá certifikát nebo tajný kód| Sledujte přihlášení instančního objektu pomocí protokolů přihlášení služby Azure AD.|
Nejde spravovat instanční objekty pomocí podmíněného přístupu.| Monitorování přihlášení pomocí protokolů přihlášení služby Azure AD
| Výchozí role Azure RBAC je Přispěvatel. |Vyhodnoťte potřeby a použijte roli s nejmenšími možnými oprávněními, aby splňovaly potřeby.|

## <a name="move-from-a-user-account-to-a-service-principal"></a>Přesun z uživatelského účtu na instanční objekt  
Pokud jako instanční objekt používáte uživatelský účet Azure, vyhodnoťte, jestli se můžete přesunout do [spravované identity](https://docs.microsoft.com/azure/app-service/overview-managed-identity?tabs=dotnet) nebo instančního objektu. Pokud nemůžete použít spravovanou identitu, zřiďte instanční objekt, který má pouze dostatečná oprávnění a rozsah ke spuštění požadovaných úloh. Instanční objekt můžete vytvořit tak, že [zaregistrujete aplikaci](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal)nebo [PowerShell](https://docs.microsoft.com/azure/active-directory/develop/howto-authenticate-service-principal-powershell).

Pokud používáte Microsoft Graph, Projděte si dokumentaci konkrétního rozhraní API, [jako v tomto příkladu](/powershell/azure/create-azure-service-principal-azureps), a ujistěte se, že typ oprávnění pro aplikaci se zobrazuje jako podporovaný.

## <a name="next-steps"></a>Další kroky

**Další informace o instančních objektech:**

[Vytvoření instančního objektu](../develop/howto-create-service-principal-portal.md)

 [Monitorování přihlašovacích objektů instančního objektu](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-sign-ins#sign-ins-report)

**Další informace o zabezpečení účtů služeb:**

[Seznámení s účty služeb Azure](service-accounts-introduction-azure.md)

[Zabezpečení spravovaných identit](service-accounts-managed-identities.md)

[Řízení účtů služeb Azure](service-accounts-governing-azure.md)

[Seznámení s místními účty služeb](service-accounts-on-premises.md)
