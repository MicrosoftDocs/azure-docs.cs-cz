---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 03/10/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: 9b4727b34bba563e9f1235771fee34273264726b
ms.sourcegitcommit: d135e9a267fe26fbb5be98d2b5fd4327d355fe97
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/10/2021
ms.locfileid: "102610678"
---
|Name<br /><sub>(Azure Portal)</sub> |Description |Vliv (s) |Verze<br /><sub>GitHubu</sub> |
|---|---|---|---|
|[Služba API Management by měla používat SKU, která podporuje virtuální sítě.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F73ef9241-5d81-4cd4-b483-8443d1730fe5) |S podporovanými SKU API Management, nasazení služby do virtuální sítě odemkne pokročilé API Management sítě a funkce zabezpečení, které poskytují větší kontrolu nad konfigurací zabezpečení sítě. Další informace najdete tady: [https://aka.ms/apimvnet](https://aka.ms/apimvnet) . |Audit, zamítnutí, zakázáno |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/API%20Management/ApiManagement_AllowedVNETSkus_AuditDeny.json) |
|[API Management služby by měly používat virtuální síť](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fef619a2c-cc4d-4d03-b2ba-8c94a834d85b) |Nasazení služby Azure Virtual Network poskytuje rozšířené zabezpečení, izolaci a umožňuje umístit službu API Management do sítě, která není v Internetu, ke které můžete řídit přístup. Tyto sítě je pak možné připojit k místním sítím pomocí různých technologií sítě VPN, což umožňuje přístup k back-endové službě v síti nebo v místním prostředí. Portál pro vývojáře a brána API je možné nakonfigurovat tak, aby byly přístupné buď z Internetu, nebo jenom v rámci virtuální sítě. |Audit, zakázáno |[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/API%20Management/ApiManagement_VNETEnabled_Audit.json) |
