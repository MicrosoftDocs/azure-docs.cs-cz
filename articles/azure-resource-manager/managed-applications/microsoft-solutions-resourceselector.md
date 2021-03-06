---
title: ResourceSelector – element uživatelského rozhraní
description: Popisuje prvek uživatelského rozhraní Microsoft. Solutions. ResourceSelector pro Azure Portal. Slouží k získání seznamu existujících prostředků.
author: tfitzmac
ms.topic: conceptual
ms.date: 07/13/2020
ms.author: tomfitz
ms.openlocfilehash: d4b21f092733f6ebb3c2bf5aa06c1d2782323730
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/09/2020
ms.locfileid: "87097274"
---
# <a name="microsoftsolutionsresourceselector-ui-element"></a>Microsoft. Solutions. ResourceSelector – element uživatelského rozhraní

ResourceSelector umožňuje uživatelům vybrat existující prostředek z předplatného.

## <a name="ui-sample"></a>Ukázka uživatelského rozhraní

![Microsoft. Solutions. ResourceSelector](./media/managed-application-elements/microsoft-solutions-resourceselector.png)

## <a name="schema"></a>Schéma

```json
{
    "name": "storageSelector",
    "type": "Microsoft.Solutions.ResourceSelector",
    "label": "Select storage accounts",
    "resourceType": "Microsoft.Storage/storageAccounts",
    "options": {
        "filter": {
            "subscription": "onBasics",
            "location": "onBasics"
        }
    }
}
```

## <a name="sample-output"></a>Ukázkový výstup

```json
"name": "{resource-name}",
"id": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/{resource-provider-namespace}/{resource-type}/{resource-name}",
"location": "{deployed-location}"
```

## <a name="remarks"></a>Poznámky

Ve `resourceType` Vlastnosti zadejte obor názvů poskytovatele prostředků a název typu prostředku pro prostředek, který chcete zobrazit v seznamu.

`filter`Vlastnost omezí dostupné možnosti pro prostředky. Výsledky můžete omezit podle umístění nebo předplatného. Chcete-li zobrazit pouze prostředky, které odpovídají výběru v základech, použijte `onBasics` . Chcete-li zobrazit všechny prostředky, použijte `all` . Výchozí hodnota je `all`.

## <a name="next-steps"></a>Další kroky

* Úvod k vytváření definic uživatelského rozhraní najdete v tématu [Začínáme s CreateUiDefinition](create-uidefinition-overview.md).
* Popis běžných vlastností v prvcích uživatelského rozhraní naleznete v tématu [CreateUiDefinition Elements](create-uidefinition-elements.md).
