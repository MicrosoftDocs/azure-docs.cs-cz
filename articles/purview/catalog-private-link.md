---
title: Použití privátních koncových bodů pro zabezpečený přístup k dosah
description: Tento článek popisuje, jak můžete nastavit privátní koncový bod pro účet dosah.
author: viseshag
ms.author: viseshag
ms.service: purview
ms.subservice: purview-data-catalog
ms.topic: how-to
ms.date: 03/02/2021
ms.openlocfilehash: d9088e5c6302c41c64f2a2e9034e7c3d659e37eb
ms.sourcegitcommit: d135e9a267fe26fbb5be98d2b5fd4327d355fe97
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/10/2021
ms.locfileid: "102615631"
---
# <a name="use-private-endpoints-for-your-purview-account"></a>Použití privátních koncových bodů pro účet dosah

Pro účty dosah můžete použít privátní koncové body, které umožní klientům a uživatelům ve virtuální síti (VNet) zabezpečeně přistupovat ke katalogu přes privátní odkaz. Privátní koncový bod používá IP adresu z adresního prostoru virtuální sítě pro váš účet dosah. Síťový provoz mezi klienty ve virtuální síti a účtem dosah se prochází přes virtuální síť a soukromým odkazem v páteřní síti Microsoftu, což eliminuje expozici veřejného Internetu.

## <a name="create-purview-account-with-a-private-endpoint"></a>Vytvoření účtu dosah pomocí privátního koncového bodu

1. Přejděte do [Azure Portal](https://portal.azure.com) a potom k účtu dosah.

1. Vyplňte základní informace a nastavte metodu připojení na privátní koncový bod na kartě **sítě** . Nastavte soukromé koncové body ingestování tím, že poskytnete podrobnosti **předplatného, virtuální sítě a podsítě** , které chcete spárovat s vaším soukromým koncovým bodem.

    :::image type="content" source="media/catalog-private-link/create-pe-azure-portal.png" alt-text="Vytvoření privátního koncového bodu v Azure Portal":::

1. Volitelně můžete také zvolit, že se má pro každý privátní koncový bod příjmu nastavit **zóna privátní DNS** .

1. Kliknutím na Přidat přidejte privátní koncový bod pro svůj účet dosah.

1. Na stránce vytvoření privátního koncového bodu nastavte dosah dílčí prostředek na **účet**, zvolte virtuální síť a podsíť a vyberte zónu privátní DNS, do které se DNS zaregistruje (můžete také využít své vyhrané servery DNS nebo vytvořit záznamy DNS pomocí hostitelských souborů na virtuálních počítačích).

    :::image type="content" source="media/catalog-private-link/create-pe-account.png" alt-text="Výběry pro vytváření privátních koncových bodů":::

1. Vyberte **OK**.

1. Vyberte **Zkontrolovat a vytvořit**. Budete přesměrováni na stránku Zkontrolovat a vytvořit, kde Azure ověří konfiguraci.

1. Jakmile se zobrazí zpráva Ověření proběhlo úspěšně, vyberte **Vytvořit**.

    :::image type="content" source="media/catalog-private-link/validation-passed.png" alt-text="Ověřování bylo úspěšné pro vytvoření účtu.":::

## <a name="create-a-private-endpoint-for-the-purview-web-portal"></a>Vytvoření privátního koncového bodu pro webový portál dosah

1. Přejděte na účet dosah, který jste právě vytvořili, a v části nastavení vyberte připojení privátního koncového bodu.

1. Kliknutím na + soukromý koncový bod vytvořte nový privátní koncový bod.

    :::image type="content" source="media/catalog-private-link/pe-portal.png" alt-text="Vytvoření privátního koncového bodu portálu":::

1. Vyplňte základní informace.

1. Na kartě prostředek vyberte typ prostředku jako **Microsoft. dosah/Accounts**.

1. Vyberte prostředek, který se má nově vytvořený účet dosah, a vyberte cílový dílčí prostředek, který má být **portál**.
    :::image type="content" source="media/catalog-private-link/pe-portal-details.png" alt-text="Podrobnosti pro soukromý koncový bod portálu":::

1. Na kartě Konfigurace vyberte virtuální síť a zónu Privátní DNS. Přejděte na stránku Souhrn a kliknutím na **vytvořit** vytvořte privátní koncový bod portálu.

## <a name="enabling-access-to-azure-active-directory"></a>Povolení přístupu k Azure Active Directory

> [!NOTE]
> Pokud má váš virtuální počítač, Brána VPN nebo brána pro partnerský vztah virtuálních sítí veřejný přístup k Internetu, může získat přístup k portálu dosah a k účtu dosah povolenému pomocí privátních koncových bodů a nemusíte přitom postupovat podle dalších pokynů níže. Pokud má vaše privátní síť pravidla skupiny zabezpečení sítě nastavená tak, aby odepřela veškerý veřejný internetový provoz, budete muset přidat některá pravidla, která umožní přístup k AAD. K tomu použijte prosím níže uvedené pokyny.

Níže uvedené pokyny slouží k zabezpečenému přístupu k dosah z virtuálního počítače Azure. Pokud používáte VPN nebo jiné brány partnerského vztahu virtuálních sítí, je potřeba, abyste se dodrželi podobný postup.

1. V Azure Portal přejděte na svůj virtuální počítač, v části nastavení vyberte kartu sítě. Pak vyberte odchozí pravidla portů a klikněte na Přidat odchozí pravidlo portu.

   :::image type="content" source="media/catalog-private-link/outbound-rule-add.png" alt-text="Přidávání odchozího pravidla":::

2. V okně Přidat pravidlo portu pro odchozí spojení vyberte možnost *cíl* , aby byla značka služby, cílová značka služby **azureactivedirectory selhala**, rozsahy cílových portů: *, akce, která má být povolena. **Priorita by měla být vyšší, než pravidlo, které zamítlo veškerý internetový provoz**. Vytvořte pravidlo.

   :::image type="content" source="media/catalog-private-link/outbound-rule-details.png" alt-text="Přidávání podrobností odchozího pravidla":::

3. Pomocí stejného postupu vytvořte další pravidlo, které povolí značku služby **AzureResourceManager**. Pokud potřebujete přístup k Azure Portal, můžete také přidat pravidlo pro značku služby *AzurePortal*.

4. Připojte se k virtuálnímu počítači, otevřete prohlížeč, přejděte do konzoly prohlížeče (Ctrl + Shift + J) a přepněte na kartu síť a sledujte síťové požadavky. Do pole Adresa URL zadejte web.purview.azure.com a zkuste se přihlásit pomocí přihlašovacích údajů AAD. Přihlášení pravděpodobně selže a na kartě síť v konzole můžete zobrazit AAD, kde se pokoušíte získat přístup k aadcdn.msauth.net, ale zablokování.

   :::image type="content" source="media/catalog-private-link/login-fail.png" alt-text="Podrobnosti neúspěšného přihlášení":::

5. V takovém případě otevřete příkazový řádek na virtuálním počítači a pomocí příkazu otestujte tuto adresu URL (aadcdn.msauth.net), Získejte IP adresu a přidejte do pravidel zabezpečení sítě virtuálního počítače pravidlo odchozího portu pro IP adresu. Nastavte cíl na IP adresu a nastavte cílové IP adresy na IP adresu aadcdn. V důsledku nástroje pro vyrovnávání zatížení a Traffic Manageru může být IP adresa AAD CDN dynamická. Jakmile obdržíte jeho IP adresu, je lepší je přidat do hostitelského souboru virtuálního počítače a vynutit tak, aby prohlížeč navštívil tuto IP adresu pro službu AAD CDN.

   :::image type="content" source="media/catalog-private-link/ping.png" alt-text="Otestovat testovací test":::

   :::image type="content" source="media/catalog-private-link/aadcdn-rule.png" alt-text="Pravidlo AAD CDN":::

6. Po vytvoření nového pravidla přejděte zpátky na virtuální počítač a zkuste se znovu přihlásit pomocí přihlašovacích údajů k AAD. Pokud je přihlášení úspěšné, portál dosah je připravený k použití. V některých případech se však AAD přesměruje na jiné domény na přihlášení na základě typu účtu zákazníka. V případě účtu live.com se AAD přesměruje na live.com na přihlašovací údaje, pak se tyto požadavky zablokují znovu. Pro účty zaměstnanců Microsoftu bude AAD k msft.sts.microsoft.com přistupovat pro přihlašovací informace. Podívejte se na kartu síťové žádosti na kartě sítě prohlížeče, kde zjistíte, které požadavky na doménu se mají zablokovat, opakujte předchozí krok, abyste získali jeho IP adresu a přidali odchozí pravidla portů ve skupině zabezpečení sítě, aby se povolily požadavky na tuto IP adresu (Pokud je to možné, přidejte do hostitelského souboru virtuálního počítače adresu URL a IP adresu pro opravu překladu DNS). Pokud znáte rozsahy IP adres v doméně přihlášení, můžete je také přímo přidat do síťových pravidel.

7. Přihlášení k AAD by teď mělo být úspěšné. Portál dosah se úspěšně načte, ale výpis všech účtů dosah nebude fungovat, protože může přistupovat jenom ke konkrétnímu účtu dosah. Pokud chcete přímo navštívit účet dosah, pro který jste úspěšně nastavili privátní koncový bod, zadejte *Web. dosah. Azure. com/Resource/{PurviewAccountName}* .

## <a name="enable-private-endpoint-on-existing-purview-accounts"></a>Povolení privátního koncového bodu u stávajících účtů dosah

Existují dva způsoby, jak můžete přidat dosah privátní koncové body po vytvoření účtu dosah:

- Použití Azure Portal (účet dosah)
- Používání centra privátních odkazů

### <a name="using-the-azure-portal-purview-account"></a>Použití Azure Portal (účet dosah)

1. V Azure Portal přejděte na účet služby dosah, v části **síť** v části **Nastavení** vyberte připojení privátního koncového bodu.

:::image type="content" source="media/catalog-private-link/pe-portal.png" alt-text="Vytvoření privátního koncového bodu portálu":::

1. Kliknutím na + soukromý koncový bod vytvořte nový privátní koncový bod.

1. Vyplňte základní informace.

1. Na kartě prostředek vyberte typ prostředku jako **Microsoft. dosah/Accounts**.

1. Vyberte prostředek, který bude účtem dosah, a vyberte cílový dílčí prostředek, který má být **účet**.

1. Na kartě Konfigurace vyberte **virtuální síť** a **zónu privátní DNS** . Přejděte na stránku Souhrn a kliknutím na **vytvořit** vytvořte privátní koncový bod portálu.

> [!NOTE]
> U cílového dílčího prostředku vybraného jako **portál** bude taky nutné postupovat podle výše uvedených kroků.

### <a name="using-the-private-link-center"></a>Používání centra privátních odkazů

1. Přejděte na [Azure Portal](https://portal.azure.com).

2. Na panelu hledání v horní části stránky vyhledejte možnost privátní odkaz a přejděte do okna privátní odkaz kliknutím na první možnost.

3. Klikněte na + Přidat a vyplňte základní podrobnosti.

   :::image type="content" source="media/catalog-private-link/private-link-center.png" alt-text="Vytvoření PE z centra privátních odkazů":::

4. Vyberte prostředek, který bude již vytvořen, a vyberte možnost cílový dílčí prostředek, který má být **účet**.

5. Na kartě Konfigurace vyberte virtuální síť a zónu Privátní DNS. Přejděte na stránku Souhrn a kliknutím na **vytvořit** vytvořte privátní koncový bod účtu.

> [!NOTE]
> U cílového dílčího prostředku vybraného jako **portál** bude taky nutné postupovat podle výše uvedených kroků.

## <a name="next-steps"></a>Další kroky

- [Procházet Data Catalog Azure dosah](how-to-browse-catalog.md)

- [Hledání ve službě Azure dosah Data Catalog](how-to-search-catalog.md)
