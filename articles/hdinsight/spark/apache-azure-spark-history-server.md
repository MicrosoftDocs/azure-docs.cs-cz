---
title: Použití rozšířených funkcí v serveru historie Apache Spark k ladění aplikací – Azure HDInsight
description: Pomocí rozšířených funkcí v serveru historie Apache Spark můžete ladit a diagnostikovat aplikace Spark – Azure HDInsight.
ms.service: hdinsight
ms.topic: how-to
ms.custom: hdinsightactive,hdiseo17may2017
ms.date: 11/25/2019
ms.openlocfilehash: 1d53d9e9ee2a7fa6588ea0993b3bebdb2a287351
ms.sourcegitcommit: 2f9f306fa5224595fa5f8ec6af498a0df4de08a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2021
ms.locfileid: "98941042"
---
# <a name="use-the-extended-features-of-the-apache-spark-history-server-to-debug-and-diagnose-spark-applications"></a>Použití rozšířených funkcí serveru historie Apache Spark k ladění a diagnostice aplikací Spark

V tomto článku se dozvíte, jak pomocí rozšířených funkcí serveru historie Apache Spark ladit a diagnostikovat dokončené nebo běžící aplikace Spark. Přípona obsahuje kartu **data** , kartu **grafu** a kartu **Diagnostika** . Na kartě **data** můžete kontrolovat vstupní a výstupní data úlohy Spark. Na kartě **graf** můžete kontrolovat tok dat a znovu spustit graf úlohy. Na kartě **Diagnostika** můžete odkazovat na funkce **analýzy překrytí** **dat**, **časové zkosení** a prováděcí modul.

## <a name="get-access-to-the-spark-history-server"></a>Získat přístup k serveru historie Spark

Server historie Spark je webové uživatelské rozhraní pro kompletní a běžící aplikace Spark. Můžete ho otevřít buď z Azure Portal, nebo z adresy URL.

### <a name="open-the-spark-history-server-web-ui-from-the-azure-portal"></a>Otevřete webové uživatelské rozhraní serveru historie Sparku z Azure Portal

1. Z [Azure Portal](https://portal.azure.com/)otevřete cluster Spark. Další informace najdete v tématech [seznam a zobrazení clusterů](../hdinsight-administer-use-portal-linux.md#showClusters).
2. Z **řídicích panelů clusteru** vyberte možnost  **Server historie Spark**. Po zobrazení výzvy zadejte přihlašovací údaje správce pro cluster Spark.

    ![Z Azure Portal spusťte server historie Spark.](./media/apache-azure-spark-history-server/azure-portal-dashboard-spark-history.png "Server historie Sparku")

### <a name="open-the-spark-history-server-web-ui-by-url"></a>Otevřete webové uživatelské rozhraní serveru historie Sparku podle adresy URL

Otevřete Server historie Sparku tak, že přejdete na `https://CLUSTERNAME.azurehdinsight.net/sparkhistory` , kde **název_clusteru** je název vašeho clusteru Spark.

Webové uživatelské rozhraní serveru historie Sparku může vypadat podobně jako na tomto obrázku:

![Stránka serveru pro historii Sparku.](./media/apache-azure-spark-history-server/hdinsight-spark-history-server.png)

## <a name="use-the-data-tab-in-the-spark-history-server"></a>Použití karty data na serveru historie Sparku

Vyberte ID úlohy a potom v nabídce Nástroje vyberte **data** , aby se zobrazila data.

+ Výběrem jednotlivých karet zkontrolujte **vstupy**, **výstupy** a **operace s tabulkami** .

    ![Karty data na stránce aplikace data pro aplikaci Spark](./media/apache-azure-spark-history-server/apache-spark-data-tabs.png)

+ Kliknutím na tlačítko **Kopírovat** zkopírujte všechny řádky.

    ![Zkopírujte data na stránce aplikace Spark.](./media/apache-azure-spark-history-server/apache-spark-data-copy.png)

+ Uložte všechna data jako. Soubor CSV výběrem tlačítka **CSV** .

    ![Uložit data jako. Soubor CSV ze stránky data pro aplikaci Spark.](./media/apache-azure-spark-history-server/apache-spark-data-save.png)

+ Vyhledejte data zadáním klíčových slov do **vyhledávacího** pole. Výsledky hledání se zobrazí okamžitě.

    ![Vyhledat data na stránce aplikace data pro aplikaci Spark.](./media/apache-azure-spark-history-server/apache-spark-data-search.png)

+ Vyberte záhlaví sloupce pro řazení tabulky. Vyberte znaménko plus pro rozbalení řádku, aby se zobrazily další podrobnosti. Vyberte znaménko mínus pro sbalení řádku.

    ![Tabulka dat na stránce data pro aplikaci Spark](./media/apache-azure-spark-history-server/apache-spark-data-table.png)

+ Pokud chcete stáhnout jeden soubor, vyberte na pravé straně tlačítko pro **částečné stažení** . Vybraný soubor se stáhne místně. Pokud soubor již neexistuje, otevře se nová karta a zobrazí se chybové zprávy.

    ![Řádek pro stažení dat na stránce data pro aplikaci Spark.](./media/apache-azure-spark-history-server/sparkui-data-download-row.png)

+ Úplnou cestu nebo relativní cestu můžete zkopírovat výběrem možnosti **Kopírovat úplnou cestu** nebo **Kopírovat relativní cestu** , která se rozšíří z nabídky stáhnout. Pro Azure Data Lake Storage soubory vyberte **otevřít v Průzkumník služby Azure Storage** a spusťte Průzkumník služby Azure Storage a vyhledejte složku po přihlášení.

    ![Zkopírujte možnosti úplná cesta a kopírovat relativní cestu na stránce aplikace data pro aplikaci Spark.](./media/apache-azure-spark-history-server/sparkui-data-copy-path.png)

+ Pokud existuje příliš mnoho řádků, které se mají zobrazit na jedné stránce, vyberte si čísla stránek v dolní části tabulky a přejděte na ni.

    ![Čísla stránek na stránce data pro aplikaci Spark](./media/apache-azure-spark-history-server/apache-spark-data-page.png)

+ Další informace získáte tak, že najedete myší nebo vyberete otazník vedle položky **data pro aplikaci Spark, kde** můžete zobrazit popis tlačítka.

    ![Získejte další informace ze stránky data pro aplikaci Spark.](./media/apache-azure-spark-history-server/sparkui-data-more-info.png)

+  Pokud chcete odeslat zpětnou vazbu k problémům, vyberte **poskytnout nám svůj názor**.

    ![Poskytněte zpětnou vazbu ze stránky data pro aplikaci Spark.](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

## <a name="use-the-graph-tab-in-the-spark-history-server"></a>Použití karty graf na serveru historie Sparku

+ Vyberte ID úlohy a potom v nabídce Nástroje vyberte **graf** . zobrazí se graf úlohy. Ve výchozím nastavení se v grafu zobrazí všechny úlohy. Vyfiltrujte výsledky pomocí rozevírací nabídky s **ID úlohy** .

    ![Rozevírací nabídka ID úlohy na stránce grafu & aplikace Spark](./media/apache-azure-spark-history-server/apache-spark-graph-jobid.png)

+ Ve výchozím nastavení je vybraný **průběh** . V rozevírací nabídce **zobrazení** vyberte **číst** nebo **napsáno** tok dat.

    ![Podívejte se na tok dat na stránce graf úlohy & aplikace Spark.](./media/apache-azure-spark-history-server/sparkui-graph-display.png)

+ Barva pozadí každého úkolu odpovídá Heat mapě.

   ![Heat mapa na stránce grafu úlohy aplikace Spark &.](./media/apache-azure-spark-history-server/sparkui-graph-heatmap.png)


    |Barva |Popis |
    |---|---|
    |Green|Úloha se úspěšně dokončila.|
    |Oranžový|Úloha se nezdařila, ale nemá vliv na konečný výsledek úlohy. Tyto úlohy mají duplicitní nebo opakované instance, které mohou být později úspěšné.|
    |Blue|Úloha je spuštěna.|
    |White|Úloha čeká na spuštění, nebo byla fáze přeskočena.|
    |Red|Úloha se nezdařila.|

     ![Spuštění úlohy na stránce grafu & aplikace Spark.](./media/apache-azure-spark-history-server/sparkui-graph-color-running.png)

     Vynechané fáze se zobrazují bíle.
    ![Přeskočená úloha na stránce grafu úlohy & aplikace Spark](./media/apache-azure-spark-history-server/sparkui-graph-color-skip.png)

    ![Neúspěšná úloha na stránce grafu & aplikace Spark](./media/apache-azure-spark-history-server/sparkui-graph-color-failed.png)

     > [!NOTE]  
     > Přehrávání je k dispozici pro dokončené úlohy. Kliknutím na tlačítko **přehrávání** přehrajte úlohu zpět. Zastavte úlohu kdykoli kliknutím na tlačítko Zastavit. Při opětovném přehrání úlohy se v každé úloze zobrazí její stav podle barvy. Přehrávání není pro nedokončené úlohy podporované.

+ Posuňte se k přiblížení nebo zmenšení grafu úlohy nebo vyberte možnost **přiblížení** , aby se vešlo na obrazovku.

    ![Vyberte možnost zvětšit, aby se vešla na stránku grafu & aplikace Spark.](./media/apache-azure-spark-history-server/sparkui-graph-zoom2fit.png)

+ Když dojde k selhání úkolů, najeďte myší na uzel grafu, aby se zobrazil popis, a pak vyberte požadovanou fázi a otevřete ji na nové stránce.

    ![Podívejte se na popis tlačítka na stránce grafu aplikace Spark & úlohy.](./media/apache-azure-spark-history-server/sparkui-graph-tooltip.png)

+ Na stránce graf & aplikace Spark se ve fázích zobrazí popisy tlačítek a malé ikony, pokud úkoly splňují tyto podmínky:
  + Zešikmení dat: velikost přečtených dat > Průměrná velikost čtení dat všech úkolů v této fázi * 2 *a* velikost pro čtení dat > 10 MB.
  + Časové zkosení: doba provádění > Průměrná doba provádění všech úkolů v této fázi * 2 *a* doba spuštění > 2 minuty.

    ![Ikona nakloněné úlohy na stránce grafu aplikace Spark & úlohy.](./media/apache-azure-spark-history-server/sparkui-graph-skew-icon.png)

+ Uzel grafu úlohy zobrazí následující informace o každé fázi:
  + ID
  + Název nebo popis
  + Celkové číslo úlohy
  + Přečtená data: součet velikosti vstupní velikosti a náhodné velikosti čtení
  + Zápis dat: součet velikosti výstupu a náhodné velikosti zápisu
  + Doba spuštění: čas mezi časem zahájení prvního pokusu a časem dokončení posledního pokusu
  + Počet řádků: součet vstupních záznamů, výstupních záznamů, náhodného čtení záznamů a náhodného zápisu záznamů
  + Průběh

    > [!NOTE]  
    > Ve výchozím nastavení bude uzel grafu úlohy zobrazovat informace z posledního pokusu o každou fázi (s výjimkou doby spuštění fáze). Během přehrávání ale uzel grafu úlohy zobrazí informace o každém pokusu.

    > [!NOTE]  
    > Pro čtení dat a velikosti zápisu dat používáme 1 MB = 1000 KB = 1000 * 1000 bajtů.

+ Pokud si chcete poslat svůj názor na problémy, vyberte **nám poskytnout zpětnou vazbu**.

    ![Možnost zpětné vazby na stránce grafu aplikace Spark & úlohy.](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

## <a name="use-the-diagnosis-tab-in-the-spark-history-server"></a>Použití karty Diagnostika na serveru historie Sparku

Vyberte ID úlohy a potom v nabídce Nástroje vyberte možnost **diagnóza** a zobrazte tak zobrazení diagnostiky úlohy. Karta **Diagnostika** zahrnuje analýzu **dat**, **zkosení času** a **analýzy využití prováděcího modulu**.

+ Vybíráním karet si Projděte přehledy o překrytí **dat**, **časovém intervalu** a **analýze využití prováděcího modulu** .

    ![Karta pro zkosení dat v rámci karty Diagnostika](./media/apache-azure-spark-history-server/sparkui-diagnosis-tabs.png)

### <a name="data-skew"></a>Zkosit data

Vyberte kartu **zkosení dat** . V závislosti na zadaných parametrech se zobrazí odpovídající zkreslené úkoly.

#### <a name="specify-parameters"></a>Zadat parametry

V části **určení parametrů** se zobrazí parametry, které se používají ke zjištění zkosení dat. Výchozí pravidlo je: načtení dat úkolu je více než třikrát průměrně přečtených dat úkolu a přečtených dat úlohy je více než 10 MB. Pokud chcete definovat vlastní pravidlo pro zkreslené úkoly, můžete zvolit parametry. Oddíly grafu **zkosených fází** a **zkosení** se budou aktualizovat odpovídajícím způsobem.

#### <a name="skewed-stage"></a>Zkosená fáze

Oddíl **zkosených fází** zobrazuje fáze, které mají úkoly, které splňují zadaná kritéria. Pokud je ve fázi více než jeden zkosený úkol, v části **zkosený fáze** se zobrazí pouze nejvýraznější úloha (tj. největší data pro zkosení dat).

![Větší zobrazení karty pro zešikmení dat na kartě Diagnostika](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section2.png)

##### <a name="skew-chart"></a>Graf zkosení

Když vyberete řádek v tabulce **fáze zkosení** , **graf zkosení** zobrazí další podrobnosti distribuce úkolů na základě doby čtení a spuštění dat. Zkreslené úkoly jsou označeny červeně a normální úlohy jsou označeny modře. Z důvodu výkonu se v grafu zobrazí ukázkové úkoly až 100. Podrobnosti o úloze se zobrazí v pravém dolním panelu.

![Graf zkosení pro fázi 10 v uživatelském rozhraní Spark](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section3.png)

### <a name="time-skew"></a>Časové zkosení

Na kartě **časové zkosení** se zobrazují zkreslené úkoly na základě doby spuštění úkolu.

#### <a name="specify-parameters"></a>Zadat parametry

V části **určení parametrů** se zobrazí parametry, které se používají k detekci asymetrie času. Výchozí pravidlo je: doba provádění úlohy je větší než třikrát Průměrná doba spuštění a doba provádění úlohy je větší než 30 sekund. Parametry můžete změnit podle svých potřeb. Graf **zkosených fází** a **zkosení** zobrazuje odpovídající informace o fázích a úlohách, stejně jako na kartě pro **zkosení dat** .

Když vyberete **časovou** osu, zobrazí se filtrovaný výsledek v části **nakloněná fáze** podle parametrů nastavených v oddílu **zadat parametry** . Když vyberete jednu položku v sekci s **šikmou fází** , bude odpovídající graf v konceptu uveden ve třetí části a v pravém dolním panelu se zobrazí podrobnosti o úloze.

![Karta časové zkosení v rámci karty Diagnostika](./media/apache-azure-spark-history-server/sparkui-diagnosis-timeskew-section2.png)

### <a name="executor-usage-analysis-graphs"></a>Grafy analýzy použití prováděcího modulu

V **grafu využití prováděcího modulu** se zobrazuje skutečným přidělením a spuštěným stavem úlohy prováděcího modulu.  

Když vyberete možnost **Analýza použití prováděcího modulu**, budou se v konceptu používat čtyři různé křivky týkající se použití prováděcího modulu: **přidělené prováděcí** moduly, **spuštěné prováděcí moduly**, **nečinné moduly** a **maximální počet instancí prováděcího** modulu. Každý **prováděcí modul** nebo událost **Odebrání prováděcího modulu** povede ke zvýšení nebo snížení přidělených prováděcích modulů. Můžete si prohlédnout **časovou osu události** na kartě **úlohy** , kde najdete další porovnání.

![Karta analýza využití prováděcího modulu v rámci karty Diagnostika](./media/apache-azure-spark-history-server/sparkui-diagnosis-executors.png)

Vyberte ikonu barvy a vyberte nebo zrušte výběr odpovídajícího obsahu ve všech konceptech.

 ![Vyberte graf na kartě analýza využití prováděcího modulu.](./media/apache-azure-spark-history-server/sparkui-diagnosis-select-chart.png)

## <a name="faq"></a>Nejčastější dotazy

### <a name="how-do-i-revert-to-the-community-version"></a>Návody se vrátit k verzi komunity?

Pokud se chcete vrátit k verzi komunity, proveďte následující kroky.

1. Otevřete cluster v Ambari.
1. Přejděte do   >  **Konfigurace** Spark2.
1. Vyberte **vlastní spark2 – výchozí**.
1. Vybrat **Přidat vlastnost...**
1. Přidejte **Spark. UI. vylepšení. Enabled = FALSE** a pak ho uložte.
1. Vlastnost nastaví na **hodnotu false** nyní.
1. Kliknutím na **Uložit** uložte konfiguraci.

    ![Vypnutí funkce v Apache Ambari](./media/apache-azure-spark-history-server/apache-spark-turn-off.png)

1. Na levém panelu vyberte **Spark2** . Pak na kartě **Souhrn** vyberte **Spark2 Server historie**.

    ![Souhrnné zobrazení v Apache Ambari](./media/apache-azure-spark-history-server/apache-spark-restart1.png)

1. Chcete-li restartovat server historie Spark, vyberte tlačítko **Start** vpravo od **serveru historie Spark2** a pak v rozevírací nabídce vyberte **restartovat** .

    ![Restartujte server historie Sparku v Apache Ambari.](./media/apache-azure-spark-history-server/apache-spark-restart2.png)  

1. Aktualizuje webové uživatelské rozhraní serveru historie Sparku. Obnoví se na verzi komunity.

### <a name="how-do-i-upload-a-spark-history-server-event-to-report-it-as-an-issue"></a>Návody nahrajte událost serveru pro historii Sparku, abyste ji nahlásili jako problém?

Pokud na serveru historie Sparku narazíte na chybu, proveďte následující kroky, které tuto událost nahlásí.

1. Stáhněte událost tak, že vyberete **Stáhnout** ve webovém uživatelském rozhraní serveru historie Spark.

    ![Stáhněte událost v uživatelském rozhraní serveru pro historii Spark.](./media/apache-azure-spark-history-server/sparkui-download-event.png)

2. Vyberte **zadat zpětnou vazbu** ze stránky **grafu & aplikace Spark** .

    ![Poskytnutí zpětné vazby na stránce grafu úlohy & aplikace Spark](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

3. Zadejte název a popis chyby. Pak přetáhněte soubor. zip do pole upravit a vyberte **Odeslat nový problém**.

    ![Odeslat a odeslat nový problém](./media/apache-azure-spark-history-server/apache-spark-file-issue.png)

### <a name="how-do-i-upgrade-a-jar-file-in-a-hotfix-scenario"></a>Návody upgradovat soubor. jar ve scénáři oprav hotfix?

Pokud chcete upgradovat pomocí opravy hotfix, použijte následující skript, který provede upgrade `spark-enhancement.jar*` .

**upgrade_spark_enhancement. sh**:

   ```bash
    #!/usr/bin/env bash

    # Copyright (C) Microsoft Corporation. All rights reserved.

    # Arguments:
    # $1 Enhancement jar path

    if [ "$#" -ne 1 ]; then
        >&2 echo "Please provide the upgrade jar path."
        exit 1
    fi

    install_jar() {
        tmp_jar_path="/tmp/spark-enhancement-hotfix-$( date +%s )"

        if wget -O "$tmp_jar_path" "$2"; then
            for FILE in "$1"/spark-enhancement*.jar
            do
                back_up_path="$FILE.original.$( date +%s )"
                echo "Back up $FILE to $back_up_path"
                mv "$FILE" "$back_up_path"
                echo "Copy the hotfix jar file from $tmp_jar_path   to $FILE"
                cp "$tmp_jar_path" "$FILE"

                "Hotfix done."
                break
            done
        else    
            >&2 echo "Download jar file failed."
            exit 1
        fi
    }

    jars_folder="/usr/hdp/current/spark2-client/jars"
    jar_path=$1

    if ls ${jars_folder}/spark-enhancement*.jar 1>/dev/null 2>&1;   then
        install_jar "$jars_folder" "$jar_path"
    else
        >&2 echo "There is no target jar on this node. Exit with no action."
        exit 0
    fi
   ```

#### <a name="usage"></a>Využití

`upgrade_spark_enhancement.sh https://${jar_path}`

#### <a name="example"></a>Příklad

`upgrade_spark_enhancement.sh https://${account_name}.blob.core.windows.net/packages/jars/spark-enhancement-${version}.jar`

#### <a name="use-the-bash-file-from-the-azure-portal"></a>Použít soubor bash z Azure Portal

1. Spusťte [Azure Portal](https://ms.portal.azure.com)a pak vyberte svůj cluster.
2. Dokončete [akci skriptu](../hdinsight-hadoop-customize-cluster-linux.md) s následujícími parametry.

    |Vlastnost |Hodnota |
    |---|---|
    |Typ skriptu|– Vlastní|
    |Name|UpgradeJar|
    |Identifikátor URI skriptu bash|`https://hdinsighttoolingstorage.blob.core.windows.net/shsscriptactions/upgrade_spark_enhancement.sh`|
    |Typ (typy) uzlů|Vedoucí pracovník|
    |Parametry|`https://${account_name}.blob.core.windows.net/packages/jars/spark-enhancement-${version}.jar`|

     ![Azure Portal odeslat akci skriptu](./media/apache-azure-spark-history-server/apache-spark-upload1.png)

## <a name="known-issues"></a>Známé problémy

+ V současné době Server historie Spark funguje jenom pro Spark 2,3 a 2,4.

+ Vstupní a výstupní data, která používají RDD, se nezobrazí na kartě **data** .

## <a name="next-steps"></a>Další kroky

+ [Správa prostředků pro cluster Apache Spark v HDInsight](apache-spark-resource-manager.md)
+ [Konfigurace nastavení Apache Sparku](apache-spark-settings.md)

## <a name="suggestions"></a>Návrhy

Pokud máte při používání tohoto nástroje nějaké připomínky nebo máte nějaké problémy, pošlete e-mail na adresu ( [hdivstool@microsoft.com](mailto:hdivstool@microsoft.com) ).
