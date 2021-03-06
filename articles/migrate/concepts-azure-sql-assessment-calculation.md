---
title: Posouzení Azure SQL v nástroji Azure Migrate Discovery and Assessment Tool
description: Další informace o hodnoceních SQL Azure v nástroji Azure Migrate Discovery and Assessment Tool
author: rashi-ms
ms.author: rajosh
ms.topic: conceptual
ms.date: 02/07/2021
ms.openlocfilehash: d1ea328575cf07a22ce39549c34d5cd21e916427
ms.sourcegitcommit: f3ec73fb5f8de72fe483995bd4bbad9b74a9cc9f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/04/2021
ms.locfileid: "102054589"
---
# <a name="assessment-overview-migrate-to-azure-sql"></a>Přehled posouzení (migrace do Azure SQL)

Tento článek poskytuje přehled posouzení pro migraci místních SQL Server instancí z prostředí VMware do databází Azure SQL nebo spravovaných instancí pomocí [nástroje Azure Migrate: Discovery and Assessment Tool](https://docs.microsoft.com/azure/migrate/migrate-services-overview#azure-migrate-server-assessment-tool).

> [!Note]
> Zjišťování a hodnocení instancí SQL Server a databází spuštěných ve vašem prostředí VMware je teď ve verzi Preview. Chcete-li vyzkoušet tuto funkci, použijte [**Tento odkaz**](https://aka.ms/AzureMigrate/SQL) k vytvoření projektu v oblasti **Austrálie – východ** . Pokud projekt již máte v Austrálii – východ a chcete si vyzkoušet tuto funkci, ujistěte se, že jste tyto [**požadavky**](how-to-discover-sql-existing-project.md) dokončili na portálu.

## <a name="whats-an-assessment"></a>Co je posouzení?
Posouzení pomocí nástroje pro zjišťování a hodnocení je časovým snímkem dat a měří připravenost a odhadne dopad migrace místních serverů do Azure.

## <a name="types-of-assessments"></a>Typy posouzení

Existují tři typy hodnocení, které můžete vytvořit pomocí nástroje Azure Migrate: zjišťování a vyhodnocení.

**Typ posouzení** | **Podrobnosti**
--- | --- 
**Virtuální počítač Azure** | Posouzení vhodnosti místních serverů k migraci na virtuální počítače Azure. Místní servery můžete vyhodnotit v prostředí [VMware](how-to-set-up-appliance-vmware.md) a [Hyper-V](how-to-set-up-appliance-hyper-v.md) a [fyzické servery](how-to-set-up-appliance-physical.md) pro migraci na virtuální počítače Azure pomocí tohoto typu posouzení.
**Azure SQL** | Vyhodnotí migraci místních SQL serverů z prostředí VMware do Azure SQL Database nebo spravované instance Azure SQL.
**Azure VMware Solution (AVS)** | Posouzení vhodnosti místních serverů k migraci do služby [Azure VMware Solution (AVS)](../azure-vmware/introduction.md). Pomocí tohoto typu posouzení můžete vyhodnotit místní [virtuální počítače VMware](how-to-set-up-appliance-vmware.md) pro migraci do řešení Azure VMware (AVS). [Další informace](concepts-azure-vmware-solution-assessment-calculation.md)

Posouzení pro Azure SQL poskytuje jedno kritérium změny velikosti:

**Kritéria stanovení velikosti** | **Podrobnosti** | **Data**
--- | --- | ---
**Na základě výkonu** | Posouzení, která poskytují doporučení na základě shromážděných údajů o výkonu | Konfigurace Azure SQL vychází z dat výkonu instancí SQL a databází, což zahrnuje: využití CPU, využití paměti, IOPS (data a soubory protokolů), propustnost a latence vstupně-výstupních operací.

## <a name="how-do-i-assess-my-on-premises-sql-servers"></a>Návody posoudit místní servery SQL?

Místní SQL Server instance můžete vyhodnotit pomocí dat o konfiguraci a využití, které shromažďuje odlehčené Azure Migrate zařízení. Zařízení zjišťuje místní instance a databáze SQL serveru a odesílá data o konfiguraci a výkonu do Azure Migrate. [Další informace](how-to-set-up-appliance-vmware.md)

## <a name="how-do-i-assess-with-the-appliance"></a>Návody posoudit pomocí zařízení?
Pokud nasazujete zařízení Azure Migrate pro zjišťování místních serverů, proveďte následující kroky:
1.  Nastavte Azure a vaše místní prostředí pro práci s Azure Migrate.
2.  Pro vaše první posouzení Vytvořte Azure Migrate projekt a přidejte do něj nástroj Azure Migrate: Discovery and Assessment.
3.  Nasaďte odlehčené zařízení Azure Migrate. Zařízení nepřetržitě zjišťuje místní servery a odesílá data o konfiguraci a výkonu Azure Migrate. Nasaďte zařízení jako virtuální počítač nebo fyzický server. Nemusíte nic instalovat na servery, které chcete vyhodnotit.

Po zahájení zjišťování zařízení můžete shromáždit servery, které chcete vyhodnotit do skupiny, a spustit posouzení pro skupinu s typem posouzení **Azure SQL**.

Postupujte podle našeho kurzu, který vyhodnotí [SQL Server instance](tutorial-assess-sql.md) pro vyzkoušení těchto kroků.

## <a name="how-does-the-appliance-calculate-performance-data-for-sql-instances-and-databases"></a>Jak zařízení počítá data o výkonu pro instance a databáze SQL?

Zařízení shromažďuje údaje o výkonu pro nastavení výpočtů pomocí těchto kroků:
1. Zařízení shromažďuje ukázkový bod v reálném čase. V případě serverů SQL Server se každých 30 sekund shromáždí vzorový bod.
2. Zařízení agreguje vzorové datové body shromážděné každých 30 sekund po dobu 10 minut. Pokud chcete vytvořit datový bod, zařízení vybere vrcholové hodnoty ze všech ukázek. Posílá maximum, průměr a rozptyl každého čítače do Azure.
3. Azure Migrate ukládá všechny datové body 10 minut za poslední měsíc.
4. Při vytváření posouzení Azure Migrate identifikuje vhodný datový bod, který se má použít pro snižování. Identifikace je založena na hodnotách percentilu pro historii výkonu a procento využití.
    - Například pokud je historie výkonu jeden týden a procento využití je 95. percentil, vyřadí hodnocení 10 minut vzorků za poslední týden. Seřadí je ve vzestupném pořadí a vybere hodnotu 95. percentilu pro snižování.
    - Hodnota 95. percentilu zajišťuje, že budete ignorovat jakékoli odlehlé hodnoty, které mohou být zahrnuty, pokud jste si vybrali 99 percentil.
    - Pokud chcete vybrat špičku pro období a nechcete vyznačit žádné odlehlé hodnoty, vyberte 99 percentil pro využití percentilu.
5. Tato hodnota se vynásobí faktorem komfortu, aby získala efektivní data o využití výkonu pro tyto metriky, které zařízení shromažďuje:
    - Využití CPU (%)
    - Využití paměti (%)
    - Čtení vstupně-výstupních operací a zápisů/s (soubory dat a protokolů)
    - Čtení MB/s a zápis MB/s (propustnost)
    - Latence vstupně-výstupních operací

## <a name="what-properties-are-used-to-create-and-customize-an-azure-sql-assessment"></a>Jaké vlastnosti se používají k vytvoření a přizpůsobení posouzení Azure SQL?

Co je je součástí vlastností posouzení Azure SQL:

**Vlastnost** | **Podrobnosti**
--- | ---
**Cílové umístění** | Oblast Azure, do které chcete migrovat. Doporučení pro konfiguraci a náklady Azure SQL jsou založená na umístění, které zadáte.
**Cílový typ nasazení** | Cílový typ nasazení, u kterého chcete spustit posouzení: vyberte **Doporučené**, pokud chcete Azure Migrate vyhodnotit připravenost vašich SQL serverů pro migraci na Azure SQL mi a Azure SQL DB a doporučit možnost nasazení s nejlepšími verzemi, cílovou vrstvou, konfigurací Azure SQL a měsíčním odhadem. Vyberte **Azure SQL DB**, pokud chcete vyhodnotit servery SQL pro migraci jenom na Azure SQL Database, a Projděte si cílovou úroveň, konfiguraci a měsíční odhady Azure SQL DB. Vyberte **Azure SQL mi**, pokud chcete vyhodnotit servery SQL pro migraci jenom na Azure SQL Database, a Projděte si cílovou úroveň, konfiguraci Azure SQL mi a měsíční odhady.
**Rezervovaná kapacita** | Určuje rezervovanou kapacitu tak, aby se odhady nákladů v posouzení braly v úvahu. Pokud vyberete možnost rezervované kapacity, nemůžete zadat "slevu" (%).
**Kritéria stanovení velikosti** | Tato vlastnost slouží ke správné velikosti konfigurace Azure SQL. Ve výchozím nastavení je to na **základě výkonu** , což znamená, že vyhodnocení bude shromažďovat metriky výkonu SQL Server instance a databáze, aby bylo možné doporučit optimální velikost spravované instance Azure SQL a/nebo Azure SQL Database doporučení na úrovni a konfiguraci.
**Historie výkonu** | Historie výkonu určuje dobu použitou při vyhodnocování údajů o výkonu.
**Percentilové využití** | Procento využití Určuje hodnotu percentilu pro vzorek výkonu, který se používá pro snižování.
**Faktor komfortu** | Vyrovnávací paměť použitá během posouzení. IT účty pro problémy, jako je sezónní využití, historie krátkého výkonu a pravděpodobná zvýšení využití v budoucnu. Například instance 10 jader s 20% využitím obvykle vede k vytvoření instance se dvěma jádry. Výsledkem je faktor komfortu 2,0, ale výsledkem je instance se čtyřmi jádry.
**Nabídka/licenční program** | [Nabídka Azure](https://azure.microsoft.com/support/legal/offer-details/) , do které jste zaregistrovaní. V současné době můžete vybírat jenom z průběžných plateb a průběžných plateb podle aktuálního využití pro vývoj/testování. Všimněte si, že můžete využít další zlevněnou kapacitu pomocí rezervované kapacity a Zvýhodněné hybridní využití Azure nad nabídkou průběžných plateb.
**Úroveň služby** | Nejvhodnější možnost úrovně služby, která bude vyhovovat vašim potřebám vaší firmy pro migraci do Azure SQL Database a/nebo spravované instance Azure SQL: Pokud chcete, aby Azure Migrate pro vaše servery doporučit nejlepší úroveň služby, vyberte **doporučeno** . To může být pro obecné účely nebo pro podnikání důležité. Vyberte možnost **pro obecné účely** , pokud chcete konfiguraci Azure SQL navrženou pro úlohy orientované na rozpočet. [Další informace](https://docs.microsoft.com/azure/azure-sql/database/service-tier-general-purpose) Vyberte **pro důležité obchodní informace** , pokud chcete, aby konfigurace Azure SQL určená pro úlohy s nízkou latencí a vysokou odolností vůči chybám a rychlému převzetí služeb při selhání. [Další informace](https://docs.microsoft.com/azure/azure-sql/database/service-tier-business-critical)
**Měna** | Fakturační měna vašeho účtu.
**Sleva (%)** | Všechny slevy specifické pro předplatné, které obdržíte nad nabídkou Azure. Výchozí nastavení je 0 %.
**Zvýhodněné hybridní využití Azure** | Určuje, zda již máte licenci SQL Server. Pokud to uděláte a jsou pokryté s aktivními softwarovými zárukami SQL Server předplatných, můžete požádat o Zvýhodněné hybridní využití Azure při přenesení licencí do Azure.

[Projděte si osvědčené postupy](best-practices-assessment.md) pro vytvoření posouzení pomocí Azure Migrate.

## <a name="calculate-readiness"></a>Vypočítat připravenost

> [!NOTE]
> Posouzení zahrnuje pouze databáze, které jsou ve stavu online. V případě, že se databáze nachází v jakémkoli jiném stavu, posouzení bude ignorovat připravenost, změnu velikosti a kalkulace nákladů pro tyto databáze. Pokud si přejete, abyste tyto databáze vyhodnotili, změňte prosím stav databáze a pokaždé přepočítejte vyhodnocení.

### <a name="azure-sql-readiness"></a>Připravenost Azure SQL

Připravenost Azure SQL pro instance a databáze SQL je založená na kontrole kompatibility funkcí s Azure SQL Database a spravovanou instancí Azure SQL:
- Posouzení Azure SQL považuje funkce instance SQL Server, které aktuálně používají zdrojové SQL Server úlohy (úlohy agenta SQL, propojené servery atd.) a schémata uživatelských databází (tabulky, zobrazení, triggery, uložené procedury atd.) a identifikují problémy s kompatibilitou.
- Pokud nejsou zjištěny žádné problémy s kompatibilitou, připravenost je označena jako **připravená** pro cílový typ nasazení (Azure SQL Database nebo Azure SQL Managed instance).
- Pokud se vyskytnou nekritické problémy s kompatibilitou, jako jsou například degradované nebo nepodporované funkce, které neblokují migraci na konkrétní cílový typ nasazení, připravenost je označena jako **připravená** (ikona s hypertextovými odkazy a modrá informace) s podrobnostmi **Upozornění** a doporučenými pokyny k nápravě.
- Pokud dojde k problémům s kompatibilitou, které mohou zablokovat migraci na konkrétní cílový typ nasazení, připravenost je označena jako **nepřipravená** s podrobnostmi o **problému** a doporučenými pokyny k nápravě.
    - Pokud existuje ještě jedna databáze v instanci SQL, která není připravena pro konkrétní cílový typ nasazení, je instance označena jako **nepřipravená** pro daný typ nasazení.
- Pokud zjišťování stále probíhá nebo dojde k potížím se zjišťováním pro instanci nebo databázi SQL, připravenost je označena jako **neznámá** , protože posouzení nemohlo vypočítat připravenost pro danou instanci SQL.

### <a name="recommended-deployment-type"></a>Doporučený typ nasazení

Pokud ve vlastnostech posouzení SQL Azure vyberete cílový typ nasazení podle **doporučení** , Azure Migrate doporučuje typ nasazení Azure SQL, který je kompatibilní s vaší instancí SQL. Migrace na cíl doporučený společností Microsoft snižuje celkovou snahu migrace. 

#### <a name="recommended-deployment-type-based-on-azure-sql-readiness"></a>Doporučený typ nasazení založený na připravenosti Azure SQL

 **Připravenost Azure SQL DB** | **Připravenost Azure SQL MI** | **Doporučený typ nasazení** | **Počítá se konfigurace Azure SQL a odhad nákladů?**
 --- | --- | --- | --- |
 Připraveno | Připraveno | Azure SQL DB nebo Azure SQL MI | Ano
 Připraveno | Nepřipraveno nebo neznámo | Azure SQL DB | Ano
 Nepřipraveno nebo neznámo | Připraveno | Azure SQL MI | Ano
 Nepřipraveno | Nepřipraveno | Potenciálně připravený pro virtuální počítač Azure | Ne
 Nepřipraveno nebo neznámo | Nepřipraveno nebo neznámo | Neznámý | Ne

> [!NOTE]
> Pokud je doporučený typ nasazení vybraný jako **doporučený** ve vlastnostech posouzení, a pokud je zdroj SQL Server dobrý pro Azure SQL DB Single Database i pro SPRAVOVANOU instanci SQL Azure, vyhodnocování doporučuje konkrétní možnost, která optimalizuje vaše náklady a vejde se do hranic velikosti a výkonu.

#### <a name="potentially-ready-for-azure-vm"></a>Potenciálně připravený pro virtuální počítač Azure

Pokud instance SQL není připravená na Azure SQL Database a Azure SQL Managed instance, doporučuje se typ nasazení označený jako *potenciálně připravený pro virtuální počítač Azure*.
- Uživatel se doporučuje vytvořit posouzení v Azure Migrate s typem posouzení jako "virtuální počítač Azure" a zjistit, jestli Server, na kterém je instance spuštěná, je připravený k migraci na virtuální počítač Azure. Poznámky:
    - Posouzení virtuálních počítačů Azure ve Azure Migrate aktuálně nasazuje a posouvá a nebere v úvahu konkrétní metriky výkonu pro provoz SQL instancí a databází na virtuálním počítači Azure. 
    - Když spustíte posouzení virtuálního počítače Azure na serveru, doporučí se Doporučené velikosti a odhad nákladů pro všechny instance běžící na serveru a můžou být migrovány na virtuální počítač Azure pomocí nástroje pro migraci serveru. Před migrací [si přečtěte pokyny pro výkon](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/performance-guidelines-best-practices) SQL Server na virtuálních počítačích Azure.


## <a name="calculate-sizing"></a>Vypočítat velikost

### <a name="azure-sql-configuration"></a>Konfigurace Azure SQL

Jakmile posouzení určí připravenost a doporučený typ nasazení Azure SQL, vypočítá konkrétní úroveň služby a konfiguraci Azure SQL (SKU velikosti), která může splňovat nebo překročit výkon místní instance SQL:
1. Během procesu zjišťování Azure Migrate shromažďuje konfiguraci a výkon instance SQL, které zahrnují:
    - Virtuální jádra (přiděleno) a využití CPU (%)
        - Využití CPU pro instanci SQL je procento přiděleného procesoru využité instancí na SQL serveru.
        - Využití CPU pro databázi je procento přiděleného procesoru využité databází v instanci SQL.
    - Paměť (přiděleno) a využití paměti (%)
    - Čtení vstupně-výstupních operací a zápisů/s (soubory dat a protokolů)
        - Čtení v/v za běhu a vstupně-výstupní operace za sekundu na úrovni instance SQL se vypočítávají přidáním vstupně-výstupních operací/s a zápisy do vstupně-výstupních operací pro všechny databáze zjištěné v této instanci.
    - Čtení MB/s a zápis MB/s (propustnost)
    - Latence vstupně-výstupních operací
    - Celková velikost databáze a organizace databázových souborů
        - Velikost databáze se vypočítá přidáním všech souborů dat a protokolů.
1. Posouzení agreguje veškerá data o konfiguraci a výkonu a snaží se najít nejlepší shodu napříč různými úrovněmi a konfiguracemi služby Azure SQL a vybere konfiguraci, která může odpovídat nebo překročí požadavky na výkon instance SQL a optimalizuje náklady.

### <a name="confidence-ratings"></a>Hodnocení spolehlivosti 
Každé posouzení služby Azure SQL je přidruženo k hodnocení spolehlivosti. Hodnocení se pohybuje od jedné (nejnižší) po pět (nejvyšší) hvězdiček. Hodnocení spolehlivosti vám pomůže odhadnout spolehlivost doporučení velikosti Azure Migrate poskytuje.
- Hodnocení spolehlivosti je přiřazeno k posouzení. Hodnocení je založeno na dostupnosti datových bodů potřebných k výpočtu posouzení.
- Pro určení velikosti na základě výkonu shromažďuje vyhodnocení údaje o výkonu všech instancí SQL a databází, mezi které patří:
    - Využití CPU (%)
    - Využití paměti (%)
    - Čtení vstupně-výstupních operací a zápisů/s (soubory dat a protokolů)
    - Čtení MB/s a zápis MB/s (propustnost)
    - Latence vstupně-výstupních operací
    
Pokud některá z těchto čísel použití nejsou k dispozici, doporučení pro velikost můžou být nespolehlivá.
Tato tabulka ukazuje hodnocení spolehlivosti, které závisí na procentu dostupných datových bodů:

**Dostupnost datového bodu** | **Hodnocení spolehlivosti**
--- | ---
0 až 20 % | 1 hvězdička
21 až 40 % | 2 hvězdičky
41 až 60 % | 3 hvězdičky
61 až 80 % | 4 hvězdičky
81 až 100 % | 5 hvězdiček

#### <a name="low-confidence-ratings"></a>Hodnocení nízké důvěry
Tady je několik důvodů, proč hodnocení může získat nízkou spolehlivost:
- Nevytvořili jste profil svého prostředí po dobu, po kterou vytváříte posouzení. Pokud například vytvoříte hodnocení s trváním výkonu nastaveným na jeden den, musíte počkat alespoň den po zahájení zjišťování všech datových bodů, které se mají shromáždit.
- Posouzení nemůže shromáždit údaje o výkonu pro některé nebo všechny servery v období posouzení. Pro hodnocení s vysokou mírou jistoty Prosím zajistěte:
    - Servery jsou napájené po dobu trvání posouzení.
    - Odchozí připojení na portech 443 jsou povolená.
    - Pokud Azure Migrate stav připojení agenta SQL v Azure Migrate je připojená a podívejte se na poslední prezenční signál 
    - Pokud je v okně zjištěná instance SQL Azure Migrate stav připojení pro všechny instance SQL "připojeno".

    Přepočítejte posouzení, aby se projevily poslední změny míry spolehlivosti.
- Některé databáze nebo instance byly vytvořeny během doby, pro kterou bylo hodnocení vypočítáno. Předpokládejme například, že jste vytvořili posouzení historie výkonu za poslední měsíc, ale některé databáze nebo instance byly vytvořeny pouze před týdnem. V takovém případě nebudou údaje o výkonu pro nové servery k dispozici po celou dobu trvání a hodnocení spolehlivosti bude nízké.

> [!NOTE]
> Protože hodnocení v Azure SQL jsou posouzení na základě výkonu, pokud je hodnocení spolehlivosti nějakého posouzení menší než pět hvězdiček, doporučujeme, abyste počkali aspoň jeden den, než zařízení profiluje prostředí a pak přepočítá hodnocení. V opačném případě může být velikost na základě výkonu nespolehlivá.

## <a name="calculate-monthly-costs"></a>Vypočítat měsíční náklady
Po dokončení doporučení pro službu Azure SQL Assessment vypočte náklady na výpočetní prostředky a úložiště pro doporučené konfigurace Azure SQL pomocí interního cenového rozhraní API. Agreguje náklady na výpočetní prostředky a úložiště napříč všemi instancemi, abyste mohli vypočítat celkové měsíční náklady na výpočetní prostředky. 
### <a name="compute-cost"></a>Náklady na výpočetní výkon
- Pro výpočet výpočetních nákladů pro konfiguraci Azure SQL se posouzení považuje za následující vlastnosti:
    - Zvýhodněné hybridní využití Azure pro licence SQL
    - Rezervovaná kapacita
    - Cílové umístění Azure
    - Měna
    - Nabídka/licenční program
    - Sleva (%)

### <a name="storage-cost"></a>Náklady na úložiště
- Odhad nákladů na úložiště zahrnuje pouze datové soubory a nikoli soubory protokolu. 
- Pro výpočet nákladů na úložiště pro konfiguraci Azure SQL se posouzení považuje za následující vlastnosti:
    - Cílové umístění Azure
    - Měna
    - Nabídka/licenční program
    - Sleva (%)
- Náklady na úložiště zálohování nejsou zahrnuté do posouzení.
- **Azure SQL Database**
    - Do odhadu nákladů se přidají minimální náklady na úložiště 5 GB a přidají se další náklady na úložiště v přírůstcích po 1 GB. [Další informace](https://azure.microsoft.com/pricing/details/sql-database/single/)
- **Spravovaná instance Azure SQL**
    - Pro první 32 GB/instanci/měsíc se nepřidaly žádné náklady na úložiště a za úložiště se přidávají další náklady na úložiště v přírůstcích 32 GB. [Další informace](https://azure.microsoft.com/pricing/details/azure-sql/sql-managed-instance/single/)
        
## <a name="next-steps"></a>Další kroky
- [Projděte si](best-practices-assessment.md) osvědčené postupy pro vytváření hodnocení. 
- Přečtěte si, jak spustit [posouzení Azure SQL](how-to-create-azure-sql-assessment.md).
