---
title: Připojení k virtuálnímu počítači SQL Azure pro indexování vyhledávání
titleSuffix: Azure Cognitive Search
description: Povolte šifrovaná připojení a nakonfigurujte bránu firewall tak, aby povolovala připojení SQL Server na virtuálním počítači Azure z indexeru v Azure Kognitivní hledání.
manager: nitinme
author: HeidiSteen
ms.author: heidist
ms.service: cognitive-search
ms.topic: conceptual
ms.date: 07/12/2020
ms.openlocfilehash: dce4c41d0d6f15ac9dc33e687c9a5ac7b7b96e06
ms.sourcegitcommit: 5f32f03eeb892bf0d023b23bd709e642d1812696
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/12/2021
ms.locfileid: "103200790"
---
# <a name="configure-a-connection-from-an-azure-cognitive-search-indexer-to-sql-server-on-an-azure-vm"></a>Konfigurace připojení ze služby Azure Kognitivní hledání indexer pro SQL Server na virtuálním počítači Azure

Jak je uvedeno v části [připojení Azure SQL Database k azure kognitivní hledání pomocí indexerů](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq), vytváření indexerů proti **SQL Server na virtuálních počítačích azure** (nebo **SQL Azure virtuálních počítačů** pro krátké) je podporované službou Azure kognitivní hledání, ale je potřeba provést několik nezbytných požadavků týkajících se zabezpečení jako první. 

Připojení z Azure Kognitivní hledání k SQL Server na virtuálním počítači je veřejné připojení k Internetu. Tady se vztahují všechny bezpečnostní míry, které byste normálně použili pro tato připojení:

+ Získejte certifikát od [poskytovatele certifikační autority](https://en.wikipedia.org/wiki/Certificate_authority#Providers) pro plně kvalifikovaný název domény instance SQL Server na virtuálním počítači Azure.
+ Nainstalujte certifikát na virtuální počítač a pak podle pokynů v tomto článku povolte a nakonfigurujte šifrovaná připojení na virtuálním počítači.

## <a name="enable-encrypted-connections"></a>Povolit šifrovaná připojení
Azure Kognitivní hledání vyžaduje šifrovaný kanál pro všechny požadavky indexeru přes veřejné internetové připojení. V této části najdete seznam kroků, které je potřeba udělat.

1. Zkontrolujte vlastnosti certifikátu a ověřte, že název subjektu je plně kvalifikovaný název domény (FQDN) virtuálního počítače Azure. K zobrazení vlastností můžete použít nástroj jako například CertUtil nebo modul snap-in Certifikáty. Plně kvalifikovaný název domény můžete získat z oddílu základy v okně služby VM, a to v poli **název veřejné IP adresy/název DNS popisek** v [Azure Portal](https://portal.azure.com/).
   
   * Pro virtuální počítače vytvořené pomocí novější šablony **Správce prostředků** je plně kvalifikovaný název domény formátovaný jako `<your-VM-name>.<region>.cloudapp.azure.com`
   * U starších virtuálních počítačů vytvořených jako **klasický** virtuální počítač je plně kvalifikovaný název domény formátovaný jako `<your-cloud-service-name.cloudapp.net>` .

2. Nakonfigurujte SQL Server k použití certifikátu pomocí Editoru registru (Regedit). 
   
    I když se pro tuto úlohu často používá SQL Server Configuration Manager, nemůžete ji použít pro tento scénář. Nenalezne importovaný certifikát, protože plně kvalifikovaný název domény virtuálního počítače v Azure se neshoduje s plně kvalifikovaným názvem domény stanoveným VIRTUÁLNÍm počítačem (doména identifikuje buď jako místní počítač, nebo do síťové domény, ke které je připojená). Pokud se názvy neshodují, určete certifikát pomocí příkazu regedit.
   
   * V nástroji Regedit přejděte do tohoto klíče registru: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate` .
     
     `[MSSQL13.MSSQLSERVER]`Část se liší v závislosti na verzi a názvu instance. 
   * Nastavte hodnotu klíče **certifikátu** na **kryptografický otisk** certifikátu TLS/SSL, který jste importovali do virtuálního počítače.
     
     Existuje několik způsobů, jak kryptografický otisk získat, což je lepší než jiné. Pokud ho zkopírujete z modulu snap-in **certifikáty** konzoly MMC, pravděpodobně si vyřadíte neviditelný úvodní znak, [jak je popsáno v tomto článku podpory](https://support.microsoft.com/kb/2023869/), což způsobí chybu při pokusu o připojení. Pro opravu tohoto problému existuje několik alternativních řešení. Nejjednodušší je místo na začátku a pak znovu zadat první znak kryptografického otisku, který odebere úvodní znak v poli hodnota klíče v regedit. Alternativně můžete použít jiný nástroj ke zkopírování kryptografického otisku.

3. Udělte oprávnění k účtu služby. 
   
    Ujistěte se, že je účtu služby SQL Server uděleno příslušné oprávnění k privátnímu klíči certifikátu TLS/SSL. Pokud přehlédnout tento krok, SQL Server se nespustí. Pro tuto úlohu můžete použít modul snap-in **certifikáty** nebo **certutil** .
    
4. Restartujte službu SQL Server.

## <a name="configure-sql-server-connectivity-in-the-vm"></a>Konfigurace připojení SQL Server ve virtuálním počítači
Po nastavení šifrovaného připojení, které vyžaduje Azure Kognitivní hledání, existují další vnitřní kroky konfigurace pro SQL Server na virtuálních počítačích Azure. Pokud jste to ještě neudělali, je dalším krokem dokončení konfigurace pomocí jednoho z těchto článků:

* **Správce prostředků** virtuálního počítače najdete v tématu [připojení k virtuálnímu počítači s SQL Server na Azure pomocí Správce prostředků](../azure-sql/virtual-machines/windows/ways-to-connect-to-sql.md). 
* Pro **klasický** virtuální počítač najdete informace v tématu [připojení k virtuálnímu počítači s SQL Server v Azure Classic](/previous-versions/azure/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect).

Konkrétně si projděte část v každém článku věnované "připojování přes Internet".

## <a name="configure-the-network-security-group-nsg"></a>Konfigurace skupiny zabezpečení sítě (NSG)
Není neobvyklé konfigurovat NSG a odpovídající koncový bod Azure ani seznam Access Control (ACL), aby váš virtuální počítač Azure byl přístupný ostatním stranám. Je pravděpodobné, že jste to udělali předtím, než povolíte vlastní aplikační logiku pro připojení k vašemu SQL Azuremu VIRTUÁLNÍmu počítači. Nejedná se o připojení Azure Kognitivní hledání k VIRTUÁLNÍmu počítači s SQL Azure. 

Odkazy níže poskytují pokyny týkající se konfigurace NSG pro nasazení virtuálních počítačů. Tyto pokyny použijte k řízení přístupu ke koncovému bodu Azure Kognitivní hledání na základě jeho IP adresy.

> [!NOTE]
> Základní informace najdete v tématu [co je skupina zabezpečení sítě](../virtual-network/network-security-groups-overview.md) .
> 
> 

* **Správce prostředků** virtuálního počítače najdete v tématu [jak vytvořit skupin zabezpečení sítě pro nasazení ARM](../virtual-network/tutorial-filter-network-traffic.md). 
* Pro **klasický** virtuální počítač si přečtěte téma [jak vytvořit skupin zabezpečení sítě pro nasazení Classic](/previous-versions/azure/virtual-network/virtual-networks-create-nsg-classic-ps).

Přidělování IP adres může představovat několik výzev, které je možné snadno překonat, pokud víte o problému a možných alternativních řešeních. Zbývající části poskytují doporučení pro zpracování problémů souvisejících s IP adresami v seznamu ACL.

#### <a name="restrict-access-to-the-azure-cognitive-search"></a>Omezení přístupu k Azure Kognitivní hledání
Důrazně doporučujeme, abyste omezili přístup k IP adrese vaší vyhledávací služby a rozsahu IP adres `AzureCognitiveSearch` [](../virtual-network/service-tags-overview.md#available-service-tags) v seznamu ACL místo toho, aby byly virtuální počítače SQL Azure otevřené pro všechny požadavky na připojení.

IP adresu můžete zjistit tak, že otestujete plně kvalifikovaný název domény (například `<your-search-service-name>.search.windows.net` ) pro vaši vyhledávací službu. I když je možné změnit IP adresu vyhledávací služby, je pravděpodobné, že se změní. IP adresa je v rámci životnosti služby obvykle statická.

Rozsah IP adres `AzureCognitiveSearch` [značky služby](../virtual-network/service-tags-overview.md#available-service-tags) můžete zjistit buď pomocí [souborů JSON ke stažení](../virtual-network/service-tags-overview.md#discover-service-tags-by-using-downloadable-json-files) , nebo přes [rozhraní API pro zjišťování značek služby](../virtual-network/service-tags-overview.md#use-the-service-tag-discovery-api-public-preview). Rozsah IP adres se aktualizuje týdně.

#### <a name="include-the-azure-cognitive-search-portal-ip-addresses"></a>Zahrnutí IP adres portálu Azure Kognitivní hledání
Pokud k vytvoření indexeru použijete Azure Portal, logika portálu Azure Kognitivní hledání také potřebuje přístup k vašemu VIRTUÁLNÍmu počítači s SQL Azure během vytváření. IP adresy portálu Azure Kognitivní hledání můžete najít pomocí nástroje Testing `stamp2.search.ext.azure.com` .

## <a name="next-steps"></a>Další kroky
Kvůli nedostatku konfigurace teď můžete jako zdroj dat pro službu Azure Kognitivní hledání indexer zadat SQL Server na virtuálním počítači Azure. Další informace najdete v tématu [připojení Azure SQL Database k Azure kognitivní hledání pomocí indexerů](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) .