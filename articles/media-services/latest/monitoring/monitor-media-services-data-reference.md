---
title: Referenční informace o Media Services dat monitorování
description: Důležité referenční materiály, které jsou potřeba při monitorování Media Services
author: IngridAtMicrosoft
ms.author: inhenkel
manager: femila
ms.topic: reference
ms.service: media-services
ms.date: 03/11/2021
ms.openlocfilehash: 461c998aa85d70d69cb267fdbeabd7eabcfb5854
ms.sourcegitcommit: 66ce33826d77416dc2e4ba5447eeb387705a6ae5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2021
ms.locfileid: "103471545"
---
# <a name="monitoring-media-services-data-reference"></a>Referenční informace o Media Services dat monitorování

Tento článek se zabývá daty, která jsou užitečná pro monitorování Media Services. Další informace o všech metrikách platforem podporovaných v Azure Monitor najdete v [Azure monitor podporované metriky](https://docs.microsoft.com/azure/azure-monitor/platform/metrics-supported).

## <a name="media-services-metrics"></a>Media Services metriky

Metriky se shromažďují v pravidelných intervalech bez ohledu na to, jestli se hodnota mění. Jsou užitečné pro upozorňování, protože je možné je vzorkovat často a výstraha se dá rychle aktivovat s relativně jednoduchou logikou.

Media Services podporuje monitorování metrik pro následující prostředky:

* Účet
* Koncový bod streamování

### <a name="account"></a>Účet

Můžete monitorovat následující metriky účtu.

|Název metriky|Zobrazované jméno|Popis|
|---|---|---|
|AssetCount|Počet assetů|Prostředky ve vašem účtu.|
|AssetQuota|Kvóta prostředků|Kvóta prostředků ve vašem účtu.|
|AssetQuotaUsedPercentage|Procento využité kvóty prostředků|Procento kvóty Assetu se už používá.|
|ContentKeyPolicyCount|Počet zásad klíče obsahu|Zásady klíčů obsahu ve vašem účtu.|
|ContentKeyPolicyQuota|Kvóta zásad pro klíč obsahu|Kvóta zásad pro klíče obsahu ve vašem účtu.|
|ContentKeyPolicyQuotaUsedPercentage|Procento využité kvóty zásad klíčů obsahu|Procento již používané kvóty zásad klíčů obsahu.|
|StreamingPolicyCount|Počet zásad streamování|Zásady streamování ve vašem účtu.|
|StreamingPolicyQuota|Kvóta zásad streamování|Kvóta zásad streamování ve vašem účtu.|
|StreamingPolicyQuotaUsedPercentage|Procento využité kvóty zásad streamování|Procento použité kvóty zásad streamování se už používá.|

Měli byste taky zkontrolovat [kvóty a omezení účtu](../limits-quotas-constraints.md).

### <a name="streaming-endpoint"></a>Koncový bod streamování

Jsou podporovány následující Media Services metriky [koncových bodů streamování](/rest/api/media/streamingendpoints) :

|Název metriky|Zobrazované jméno|Popis|
|---|---|---|
|Žádosti|Žádosti|Poskytuje celkový počet požadavků HTTP poskytovaných koncovým bodem streamování.|
|Výchozí přenos dat|Výchozí přenos dat|Celkový počet odchozích bajtů za minutu na koncový bod streamování.|
|SuccessE2ELatency|Koncová latence úspěch|Doba trvání od okamžiku, kdy koncový bod streamování přijal požadavek na odeslání posledního bajtu odpovědi.|
|Využití procesoru| | Využití procesoru pro koncové body streamování Premium Tato data nejsou k dispozici pro standardní koncové body streamování. |
|Šířka pásma pro výstup | | Šířka pásma pro odchozí přenosy v bitech za sekundu|

## <a name="metric-dimensions"></a>Dimenze metriky

Další informace o tom, jaké dimenze metriky jsou, najdete v tématu multidimenzionální [metriky](https://docs.microsoft.com/azure/azure-monitor/platform/data-platform-metrics#multi-dimensional-metrics).

<!--**PLACEHOLDER** for dimensions table.-->

## <a name="resource-logs"></a>Protokoly prostředků

## <a name="media-services-diagnostic-logs"></a>Protokoly diagnostiky Media Services

Diagnostické protokoly poskytují bohatou a častou data o provozu prostředku Azure. Další informace najdete v tématu [Jak shromažďovat a využívat data protokolu z vašich prostředků Azure](https://docs.microsoft.com/azure/azure-monitor/essentials/platform-logs-overview.md).

Media Services podporuje následující diagnostické protokoly:

* Doručení klíče

### <a name="key-delivery"></a>Doručení klíče

|Název|Popis|
|---|---|
|Požadavek služby doručení klíčů|Protokoly, které zobrazují informace o požadavku služby doručování klíčů Další informace najdete v tématu [schémata](monitor-media-services-data-reference.md).|

## <a name="schemas"></a>Schémata

Podrobný popis schématu diagnostických protokolů nejvyšší úrovně najdete v tématu [podporované služby, schémata a kategorie pro diagnostické protokoly Azure](https://docs.microsoft.com/azure/azure-monitor/essentials/resource-logs-schema.md).

## <a name="key-delivery-log-schema-properties"></a>Vlastnosti schématu protokolu doručení klíčů

Tyto vlastnosti jsou specifické pro schéma protokolu doručení klíčů.

|Název|Popis|
|---|---|
|keyId|ID požadovaného klíče|
|keyType|Může to být jedna z následujících hodnot: "Clear" (bez šifrování), "FairPlay", "PlayReady" nebo "Widevine".|
|policyName|Azure Resource Manager název zásady.|
|Typ TokenType|Typ tokenu.|
|statusMessage|Stavová zpráva|

### <a name="example"></a>Příklad

Vlastnosti schématu žádostí o doručení klíčů

```json
{
    "time": "2019-01-11T17:59:10.4908614Z",
    "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-0000000000/RESOURCEGROUPS/SBKEY/PROVIDERS/MICROSOFT.MEDIA/MEDIASERVICES/SBDNSTEST",
    "operationName": "MICROSOFT.MEDIA/MEDIASERVICES/CONTENTKEYS/READ",
    "operationVersion": "1.0",
    "category": "KeyDeliveryRequests",
    "resultType": "Succeeded",
    "resultSignature": "OK",
    "durationMs": 315,
    "identity": {
        "authorization": {
            "issuer": "http://testacs",
            "audience": "urn:test"
        },
        "claims": {
            "urn:microsoft:azure:mediaservices:contentkeyidentifier": "3321e646-78d0-4896-84ec-c7b98eddfca5",
            "iss": "http://testacs",
            "aud": "urn:test",
            "exp": "1547233138"
        }
    },
    "level": "Informational",
    "location": "uswestcentral",
    "properties": {
        "requestId": "b0243468-d8e5-4edf-a48b-d408e1661050",
        "keyType": "Clear",
        "keyId": "3321e646-78d0-4896-84ec-c7b98eddfca5",
        "policyName": "56a70229-82d0-4174-82bc-e9d3b14e5dbf",
        "tokenType": "JWT",
        "statusMessage": "OK"
    }
} 
```

```json
 {
    "time": "2019-01-11T17:59:33.4676382Z",
    "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-0000000000/RESOURCEGROUPS/SBKEY/PROVIDERS/MICROSOFT.MEDIA/MEDIASERVICES/SBDNSTEST",
    "operationName": "MICROSOFT.MEDIA/MEDIASERVICES/CONTENTKEYS/READ",
    "operationVersion": "1.0",
    "category": "KeyDeliveryRequests",
    "resultType": "Failed",
    "resultSignature": "Unauthorized",
    "durationMs": 2,
    "level": "Error",
    "location": "uswestcentral",
    "properties": {
        "requestId": "875af030-b77c-416b-b7e1-58f23ebec182",
        "keyType": "Clear",
        "keyId": "3321e646-78d0-4896-84ec-c7b98eddfca5",
        "policyName": "56a70229-82d0-4174-82bc-e9d3b14e5dbf",
        "tokenType": "None",
        "statusMessage": "No token present in authorization header or URL."
    }
} 
```

>[!NOTE]
> Widevine je služba od společnosti Google Inc. v souladu s podmínkami služby a zásadami ochrany osobních údajů Google, Inc.

## <a name="next-steps"></a>Další kroky

[!INCLUDE [monitoring-next-steps](../includes/monitoring-next-steps.md)]
