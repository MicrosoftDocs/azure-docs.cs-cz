---
title: Aktualizace dat analýzy hrozeb
description: Datový balíček Analýza hrozeb je k dispozici pro každý nový Defender pro verzi IoT nebo v případě potřeby mezi verzemi.
author: shhazam-ms
manager: rkarlin
ms.author: shhazam
ms.date: 12/14/2020
ms.service: azure
ms.topic: how-to
ms.openlocfilehash: a210771d99d28a0e9c15d7952d491a5e5f94e704
ms.sourcegitcommit: 27d616319a4f57eb8188d1b9d9d793a14baadbc3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/15/2021
ms.locfileid: "100521403"
---
# <a name="threat-intelligence-research-and-packages"></a>Analýzy a balíčky pro analýzu hrozeb

Týmy zabezpečení v Microsoftu provádějí proprietární vlastní funkce a analýzy ohrožení zabezpečení ICS. Mezi tyto týmy patří MSTIC (Microsoft Threat Intelligence Center), DART (Microsoft Detection and Response Team), DCU (digitální zločiny) a oddíl 52 (odborníci na doménu IoT/pro/ICS, kteří sledují nulové dny v oblasti ICS, zpětného strojírenství malwaru, kampaně a nežádoucí osoby).

Týmy poskytují detekci, analýzu a reakci na zabezpečení Microsoftu:

- Cloudová infrastruktura a služby.
- Tradiční produkty a zařízení.
- Interní podnikové prostředky.

Týmy zabezpečení získají výhody pro:

- Ochrana před známými a relevantními hrozbami.
- Přehledy, které vám pomůžou při třídění a stanovení priorit.
- Porozumění úplnému kontextu hrozeb před tím, než se to týká.
- Relevantnější, přesné a napadnutelná data.

Tato funkce poskytuje informace o kontextu pro rozšíření analýzy platformy Microsoft a podporuje spravované služby společnosti za účelem reakce na incidenty a vyšetřování porušení zabezpečení. Balíčky analýzy hrozeb obsahují signatury (včetně signatur malwaru), CVEs a další obsah zabezpečení.

Balíčky můžete stáhnout ze stránky **aktualizace** na portálu Azure Defender pro IoT Portal.

:::image type="content" source="media/how-to-work-with-threat-intelligence-packages/download-screen.png" alt-text="Stáhněte si aktualizace prostřednictvím Azure Defenderu pro IoT Portal.":::

## <a name="update-threat-intelligence-data"></a>Aktualizace dat analýzy hrozeb

Balíčky analýzy hrozeb jsou k dispozici pro každý nový Defender pro aktualizaci verze IoT nebo v případě potřeby mezi verzemi.

Balíčky, které stáhnete z programu Defender pro IoT Portal, se dají ručně nahrát na jednotlivé senzory. Pokud místní Konzola pro správu spravuje vaše senzory, můžete si stáhnout balíčky pro analýzy hrozeb do konzoly pro správu a současně je vložit do více senzorů.

Aktualizace balíčku na jednom snímači:

1. Přejít na stránku **aktualizace** pro Azure Defender pro IoT.

2. Stáhněte a uložte balíček pro **analýzu hrozeb** .

3. Přihlaste se ke konzole senzorů.

4. V postranní nabídce vyberte **nastavení systému**.

5. Vyberte **data analýzy hrozeb** a pak vyberte **aktualizovat**.

6. Nahrajte nový balíček.

Postup aktualizace balíčku na více senzorech současně:

1. Přejít na stránku **aktualizace** pro Azure Defender pro IoT.

2. Stáhněte a uložte balíček pro **analýzu hrozeb** .

3. Přihlaste se ke konzole pro správu.

4. V postranní nabídce vyberte **nastavení systému**.

5. V části **Konfigurace modulu senzorů** vyberte senzory, které by měly dostávat aktualizované balíčky.  

6. V části **Vybrat data analýzy hrozeb** vyberte znaménko plus ( **+** ).

7. Nahrajte balíček.

## <a name="next-steps"></a>Další kroky

[Aktualizované verze](how-to-manage-sensors-from-the-on-premises-management-console.md#update-versions)
