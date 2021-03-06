---
author: MikeRayMSFT
ms.service: azure-arc
ms.subservice: azure-arc-data
ms.topic: include
ms.date: 03/02/2021
ms.author: mikeray
ms.openlocfilehash: 0fca43f76b24a08ca96be749f7f2a822b0be2418
ms.sourcegitcommit: c27a20b278f2ac758447418ea4c8c61e27927d6a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/03/2021
ms.locfileid: "101687582"
---
V této části se dozvíte, jak použít omezení kontextu zabezpečení (SCC). Pro verzi Preview tyto omezení zabezpečení neuvolní. 

1. Stáhněte si omezení vlastního kontextu zabezpečení (SCC). Použijte jednu z následujících možností: 
   - [GitHub](https://github.com/microsoft/azure_arc/tree/main/arc_data_services/deploy/yaml/arc-data-scc.yaml) 
   - [Žádný](https://raw.githubusercontent.com/microsoft/azure_arc/main/arc_data_services/deploy/yaml/arc-data-scc.yaml)
   - `curl`
   
      Následující příkaz stáhne oblouk-data-SCC. yaml:

      ```console
      curl https://raw.githubusercontent.com/microsoft/azure_arc/main/arc_data_services/deploy/yaml/arc-data-scc.yaml -o arc-data-scc.yaml
      ```

1. Vytvořte SCC.

   ```console
   oc create -f arc-data-scc.yaml
   ```

1. Použijte SCC pro účet služby.

   > [!NOTE]
   > Použijte stejný obor názvů a v `azdata arc dc create` níže uvedeném příkazu. Příklad je `arc` .

   ```console
   oc adm policy add-scc-to-user arc-data-scc --serviceaccount default --namespace arc
   ```

   ```console
   oc create rolebinding arc-data-rbac --clusterrole=system:openshift:scc:arc-data-scc --serviceaccount=arc:default
   ```
