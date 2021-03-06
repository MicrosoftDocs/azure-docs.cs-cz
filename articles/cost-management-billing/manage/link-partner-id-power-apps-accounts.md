---
title: Propojit ID partnera s vašimi účty Power Apps s přihlašovacími údaji Azure
description: Tento článek pomáhá partnerům Microsoftu používat svoje přihlašovací údaje Azure k tomu, aby zákazníkům pomohl používat aplikace Microsoft Power Apps.
author: bandersmsft
ms.reviewer: akangaw
ms.service: cost-management-billing
ms.subservice: billing
ms.topic: conceptual
ms.date: 03/16/2021
ms.author: banders
ms.openlocfilehash: adaff7a6b8559fe9604412a44eced6c490231e3c
ms.sourcegitcommit: 27cd3e515fee7821807c03e64ce8ac2dd2dd82d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2021
ms.locfileid: "103603819"
---
# <a name="link-a-partner-id-to-your-power-apps-accounts"></a>Propojení ID partnera s účty Power Apps

Tento článek pomáhá partnerům Microsoftu, kteří jsou poskytovateli služeb Power Apps, přidružit službu ke zákazníkům v aplikacích Microsoft Power Apps. Když (partner Microsoftu) spravuje, konfiguruje a podporuje služby Power Apps pro zákazníka, máte přístup k prostředí vašeho zákazníka. K přidružení ID partnerské sítě k účtu, který se používá pro doručování služeb, můžete použít přihlašovací údaje Azure a odkaz na partnerského správce (PAL).

PAL umožňuje Microsoftu identifikovat a rozpoznávat partnery, kteří mají zákazníky Power Apps. Použití atributů Microsoftu pro organizaci partnera na základě oprávnění účtu (role Power Apps) a oboru (tenant, skupina prostředků, prostředek).

## <a name="get-access-from-your-customer"></a>Získání přístupu od zákazníka

Před propojením ID partnera vám zákazník musí udělit přístup k prostředkům Power Apps pomocí jedné z následujících možností:

- **Uživatel typu Host** – váš zákazník vám může přidat jako uživatele typu Host a přiřadit libovolné role Power Apps. Další informace najdete v tématu [Přidání uživatelů typu host z jiného adresáře](../../active-directory/external-identities/what-is-b2b.md).
- **Účet adresáře** – váš zákazník může vytvořit uživatelský účet ve vlastním adresáři a přiřadit libovolné role Power Apps.
- **Instanční objekt** : zákazník může přidat aplikaci nebo skript z vaší organizace do svého adresáře a přiřadit libovolné role Power Apps. Identita aplikace nebo skriptu se označuje jako instanční objekt.
- **Delegovaný správce** – váš zákazník může delegovat skupinu prostředků, aby na ní uživatelé mohli pracovat v rámci vašeho tenanta. Další informace najdete v tématu [pro partnery: delegovaný správce](/power-platform/admin/for-partners-delegated-administrator).

## <a name="link-customer-to-a-partner-id"></a>Propojit zákazníka s ID partnera

Když máte přístup k prostředkům vašeho zákazníka, pomocí Azure Portal, PowerShellu nebo rozhraní příkazového řádku Azure můžete propojit ID Microsoft Partner Network (MPN ID) s vaším ID uživatele nebo instančním objektem. Propojte ID partnera s každým klientem zákazníka.

### <a name="use-the-azure-portal-to-link-to-a-new-partner-id"></a>Použití webu Azure Portal k propojení s novým ID partnera

1. Přihlaste se na [Azure Portal](https://portal.azure.com).
1. Na webu Azure Portal přejděte na [Propojit s ID partnera](https://portal.azure.com/#blade/Microsoft_Azure_Billing/managementpartnerblade).
1. Zadejte ID [Microsoft Partner Network](https://partner.microsoft.com/) vaší organizaci. Nezapomeňte použít  **přidružené ID MPN**  , které vidíte na vašem partnerském profilu.  
    :::image type="content" source="./media/link-partner-id-power-apps-accounts/link-partner-id.png" alt-text="Snímek obrazovky zobrazující odkaz na okno ID partnera" lightbox="./media/link-partner-id-power-apps-accounts/link-partner-id.png" :::
1. Pokud chcete propojit ID partnera s jiným zákazníkem, přepněte adresář. V části **Přepnout adresář** vyberte příslušný adresář.  
    :::image type="content" source="./media/link-partner-id-power-apps-accounts/switch-directory.png" alt-text="Snímek obrazovky s oknem adresář + předplatné, kde můžete přepnout svůj adresář" lightbox="./media/link-partner-id-power-apps-accounts/switch-directory.png" :::

### <a name="use-powershell-to-link-to-a-new-partner-id"></a>Použití PowerShellu k propojení s novým ID partnera

Nainstalujte modul Azure PowerShell [AZ. ManagementPartner](https://www.powershellgallery.com/packages/Az.ManagementPartner/) .

Přihlaste se k tenantovi zákazníka pomocí uživatelského účtu nebo instančního objektu. Další informace najdete v tématu [Přihlášení pomocí Azure PowerShellu](/powershell/azure/authenticate-azureps).

```azurepowershell-interactive
Update-AzManagementPartner -PartnerId 12345
```

Vytvořte propojení s novým ID partnera. ID partnera je ID programu [Microsoft Partner Network](https://partner.microsoft.com/) pro vaši organizaci. Nezapomeňte použít **přidružené ID MPN**  , které vidíte na vašem partnerském profilu.

```azurepowershell-interactive
new-AzManagementPartner -PartnerId 12345
```

Získání propojeného ID partnera

```azurepowershell-interactive
get-AzManagementPartner
```

Aktualizace propojeného ID partnera

```azurepowershell-interactive
Update-AzManagementPartner -PartnerId 12345
```

Odstranění propojeného ID partnera

```azurepowershell-interactive
remove-AzManagementPartner -PartnerId 12345
```

### <a name="use-the-azure-cli-to-link-to-a-new-partner-id"></a>Použití Azure CLI k propojení s novým ID partnera

Nejdřív nainstalujte rozšíření Azure CLI.

```azurecli-interactive
az extension add --name managementpartner
```

Přihlaste se k tenantovi zákazníka pomocí uživatelského účtu nebo instančního objektu. Další informace najdete v tématu [Přihlášení pomocí Azure CLI](/cli/azure/authenticate-azure-cli).

```azurecli-interactive
az login --tenant TenantName
```

Vytvořte propojení s novým ID partnera. ID partnera je ID programu [Microsoft Partner Network](https://partner.microsoft.com/) pro vaši organizaci.

```azurecli-interactive
az managementpartner create --partner-id 12345
```

Získání propojeného ID partnera

```azurecli-interactive
az managementpartner show
```

Aktualizace propojeného ID partnera

```azurecli-interactive
az managementpartner update --partner-id 12345
```

Odstranění propojeného ID partnera

```azurecli-interactive
az managementpartner delete --partner-id 12345
```

## <a name="frequently-asked-questions-faq"></a>Nejčastější dotazy

Následující části obsahují Nejčastější dotazy týkající se propojení ID partnera s účty Power Apps.

### <a name="who-should-link-the-partner-id"></a>Kdo má propojit ID partnera?

Každý uživatel z partnerské organizace, který pracuje na zdrojích Power Apps zákazníka, může propojit ID partnera s účtem. V ideálním případě by přidružení v PAL mělo být provedeno na začátku projektu. Dá se ale udělat vždycky, když máte přístup v adresáři zákazníka.

### <a name="can-a-partner-id-be-changed-after-its-linked"></a>Je možné po propojení změnit ID partnera?

Ano. Propojené ID partnera lze změnit, přidat nebo odebrat. Příkladem pro tuto situaci může být situace, kdy zaměstnanec z vaší společnosti opustí vaši organizaci. Dalším příkladem může být situace, kdy projekt nebo smlouva s zákazníkem skončí.

### <a name="what-if-a-user-has-an-account-in-more-than-one-customer-tenant"></a>Co když má uživatel účet ve více než jednom tenantovi zákazníka?

Propojení mezi ID partnera a účtem se provádí u každého tenanta zákazníka. Propojte toto ID partnera v každém tenantovi zákazníka.

### <a name="can-other-partners-or-customers-edit-or-remove-the-link-to-the-partner-id"></a>Můžou propojení s ID partnera upravit nebo odebrat jiní partneři nebo zákazníci?

Propojení je přiřazeno na úrovni uživatelského účtu. Propojení s ID partnera můžete upravit nebo odebrat jenom vy. Zákazník ani jiní partneři nemůžou propojení s ID partnera změnit.

### <a name="which-mpn-id-should-i-use-if-my-company-has-multiple"></a>Které MPN ID mám použít, pokud jich má moje společnost více?

Nezapomeňte použít **přidružené ID MPN**, které je uvedené ve vašem partnerském profilu. Obvykle se jedná o přidružení ID místního účtu k vaší organizaci.

### <a name="how-do-i-explain-pal-to-my-customer"></a>Vysvětlete si Návody zákazníka?

PAL umožňuje Microsoftu identifikovat a rozpoznat partnery, kteří pomáhají zákazníkům dosáhnout obchodních cílů a realizace hodnoty v cloudu. Zákazníci musí nejdřív poskytnout přístup k partnerům jejich prostředků Power Apps. Po udělení přístupu se k němu přidělí ID Microsoft Partner Network partnera (MPN ID). Toto přidružení pomáhá Microsoftu porozumět poskytovatelům služeb a zdokonalovat nástroje a programy potřebné k tomu, aby zákazníci mohli nejlépe podporovat.

### <a name="what-data-does-pal-collect"></a>Jaká data shromažďuje PAL?

Přidružení PAL k existujícím přihlašovacím údajům neposkytuje Microsoftu žádná nová zákaznická data. Poskytne Microsoftu informace o tom, kde je partner aktivně zapojen do prostředí Power Apps zákazníka. Microsoft může na základě oprávnění účtu (role Power Apps) a rozsahu (tenanta, skupiny prostředků, prostředku) poskytnout partnerovi od zákazníka jeho využití a vliv z prostředí zákazníka na partnerský subjekt.

### <a name="does-pal-association-affect-the-security-of-a-customers-power-apps-environment"></a>Ovlivňuje přidružení PAL zabezpečení prostředí Power Apps zákazníka?

Asociace PAL přidává ID MPN partnera jenom na přihlašovací údaje, které jsou už zřízené. Nemění oprávnění (role Power Apps) ani neposkytují partnerům nebo Microsoftu dodatečná data služby Power Apps.

### <a name="next-steps"></a>Další kroky

- Připojte se k diskuzi v [komunitě partnerů Microsoftu](https://aka.ms/PALdiscussion), abyste mohli dostávat aktualizace nebo odesílat zpětnou vazbu.
- Přečtěte si [Nejčastější dotazy k aplikaci pro vývoj aplikací s nízkým kódem](https://assetsprod.microsoft.com/mpn/faq-low-code-app-development-advanced-specialization.pdf) pro přidružení Power Apps založené na PAL pro pokročilou specializaci vývoj aplikací s nízkým kódem.
