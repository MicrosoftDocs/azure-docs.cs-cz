---
title: Ukázky šablon Správce prostředků pro pravidla shromažďování dat
description: Ukázka Azure Resource Manager šablon pro vytváření přidružení mezi pravidly shromažďování dat a virtuálními počítači v Azure Monitor.
ms.topic: sample
author: bwren
ms.author: bwren
ms.date: 11/17/2020
ms.openlocfilehash: 5ceaaa7ed9288299019f3e87d8c214e53013f5ec
ms.sourcegitcommit: f3ec73fb5f8de72fe483995bd4bbad9b74a9cc9f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/04/2021
ms.locfileid: "102045747"
---
# <a name="resource-manager-template-samples-for-data-collection-rules-in-azure-monitor"></a>Ukázky šablon Správce prostředků pro pravidla shromažďování dat v Azure Monitor
Tento článek obsahuje ukázkové [Azure Resource Manager šablony](../../azure-resource-manager/templates/template-syntax.md) pro nasazení a konfiguraci [agenta Log Analytics](./log-analytics-agent.md) a [rozšíření diagnostiky](./diagnostics-extension-overview.md) pro virtuální počítače v Azure monitor. Každá ukázka obsahuje soubor šablony a soubor parametrů s ukázkovými hodnotami, které se mají poskytnout šabloně.

[!INCLUDE [azure-monitor-samples](../../../includes/azure-monitor-resource-manager-samples.md)]


## <a name="create-association-with-azure-vm"></a>Vytvoření asociace s virtuálním počítačem Azure

Následující příklad vytvoří přidružení mezi virtuálním počítačem Azure a pravidlem shromažďování dat.

### <a name="template-file"></a>Soubor šablony

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "vmName": {
            "type": "string",
            "metadata": {
                "description": "Name of the virtual machine."
            }
        },
        "associationName": {
            "type": "string",
            "metadata": {
                "description": "Name of the association."
            }
        },
        "dataCollectionRuleId": {
            "type": "string",
            "metadata": {
                "description": "Resource ID of the data collection rule."
            }
        }
    },
    "resources": [
        {
            "type": "Microsoft.Compute/virtualMachines/providers/dataCollectionRuleAssociations",
            "name": "[concat(parameters('vmName'),'/microsoft.insights/', parameters('associationName'))]",
            "apiVersion": "2019-11-01-preview",
            "properties": {
                "description": "Association of data collection rule. Deleting this association will break the data collection for this virtual machine.",
                "dataCollectionRuleId": "[parameters('dataCollectionRuleId')]"
            }
        }
    ]
}
```

### <a name="parameter-file"></a>Soubor parametrů

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "vmName": {
        "value": "my-windows-vm"
      },
      "location": {
        "value": "eastus"
      }
  }
}
```

## <a name="create-association-with-azure-arc"></a>Vytvoření asociace pomocí ARC Azure

Následující ukázka vytvoří přidružení mezi serverem s podporou ARC Azure a pravidlem shromažďování dat.

### <a name="template-file"></a>Soubor šablony

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "vmName": {
            "type": "string",
            "metadata": {
                "description": "Name of the virtual machine."
            }
        },
        "associationName": {
            "type": "string",
            "metadata": {
                "description": "Name of the association."
            }
        },
        "dataCollectionRuleId": {
            "type": "string",
            "metadata": {
                "description": "Resource ID of the data collection rule."
            }
        }
    },
    "resources": [
        {
            "type": "Microsoft.HybridCompute/machines/providers/dataCollectionRuleAssociations",
            "name": "[concat(parameters('machineName'),'/microsoft.insights/', parameters('associationName'))]",
            "apiVersion": "2019-11-01-preview",
            "properties": {
                "description": "Association of data collection rule. Deleting this association will break the data collection for this Arc server.",
                "dataCollectionRuleId": "[parameters('dataCollectionRuleId')]"
            }
        }
    ]
}
```

### <a name="parameter-file"></a>Soubor parametrů

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "vmName": {
        "value": "my-windows-vm"
      },
      "location": {
        "value": "eastus"
      }
  }
}
```


## <a name="next-steps"></a>Další kroky

* [Získejte další ukázkové šablony pro Azure monitor](../resource-manager-samples.md).
* [Přečtěte si další informace o agentovi Log Analytics](./log-analytics-agent.md).
* [Přečtěte si další informace o diagnostickém rozšíření](./diagnostics-extension-overview.md).