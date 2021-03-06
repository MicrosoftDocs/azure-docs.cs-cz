---
title: IT Service Management Connector – zabezpečení exportu v Azure Monitor – konfigurace pomocí ServiceNow
description: V tomto článku se dozvíte, jak připojit ITSM produkty/služby k ServiceNow při zabezpečeném exportu v Azure Monitor.
ms.topic: conceptual
author: nolavime
ms.author: v-jysur
ms.date: 12/31/2020
ms.openlocfilehash: cf19911bd8126bfb73f848c086aa817a7d7adb00
ms.sourcegitcommit: 18a91f7fe1432ee09efafd5bd29a181e038cee05
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2021
ms.locfileid: "103563687"
---
# <a name="connect-servicenow-to-azure-monitor"></a>Připojení ServiceNow k Azure Monitor

Následující části obsahují podrobné informace o tom, jak připojit produkt ServiceNow a zabezpečený export v Azure.

## <a name="prerequisites"></a>Požadavky

Ujistěte se, že jste splnili následující požadavky:

* Služba Azure AD je zaregistrovaná.
* Máte podporovanou verzi správy událostí ServiceNow-ITOM (verze New York nebo novější).
* [Aplikace](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ac4c9c57dbb1d090561b186c1396191a/1.3.1?referer=%2Fstore%2Fsearch%3Flistingtype%3Dallintegrations%25253Bancillary_app%25253Bcertified_apps%25253Bcontent%25253Bindustry_solution%25253Boem%25253Butility%26q%3DEvent%2520Management%2520Connectors&sl=sh) je nainstalovaná v instanci ServiceNow.

## <a name="configure-the-servicenow-connection"></a>Konfigurace připojení ServiceNow

1. Pro definici zabezpečeného exportu použijte linku https://(název instance). Service-Now. com/API/sn_em_connector/em/inbound_event? source = azuremonitor identifikátor URI.

2. Postupujte podle pokynů podle verze:
   * [Paříž](https://docs.servicenow.com/bundle/paris-it-operations-management/page/product/event-management/concept/azure-integration.html)
   * [Orlandu](https://docs.servicenow.com/bundle/orlando-it-operations-management/page/product/event-management/concept/azure-integration.html)
   * [New York](https://docs.servicenow.com/bundle/newyork-it-operations-management/page/product/event-management/concept/azure-integration.html)
