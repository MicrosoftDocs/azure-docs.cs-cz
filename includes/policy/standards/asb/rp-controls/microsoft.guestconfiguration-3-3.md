---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 03/10/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: c495e2f25f9e55fc3147ca4c8bcddf51288865ea
ms.sourcegitcommit: b572ce40f979ebfb75e1039b95cea7fce1a83452
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2021
ms.locfileid: "103021551"
---
|Name<br /><sub>(Azure Portal)</sub> |Description |Vliv (s) |Verze<br /><sub>GitHubu</sub> |
|---|---|---|---|
|[Audit počítačů s Windows chybějících zadaných členů ve skupině Administrators](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F30f71ea1-ac77-4f26-9fc5-2d926bbd4ba7) |Vyžaduje nasazení požadovaných požadavků do oboru přiřazení zásad. Podrobnosti najdete na adrese [https://aka.ms/gcpol](https://aka.ms/gcpol) . Počítače jsou nekompatibilní, pokud místní skupina Administrators neobsahuje jednoho nebo více členů uvedených v parametru zásad. |auditIfNotExists |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Guest%20Configuration/GuestConfiguration_AdministratorsGroupMembersToInclude_AINE.json) |
|[Auditovat počítače s Windows, které mají další účty ve skupině Administrators](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F3d2a3320-2a72-4c67-ac5f-caa40fbee2b2) |Vyžaduje nasazení požadovaných požadavků do oboru přiřazení zásad. Podrobnosti najdete na adrese [https://aka.ms/gcpol](https://aka.ms/gcpol) . Počítače jsou nekompatibilní, pokud místní skupina Administrators obsahuje členy, kteří nejsou uvedeni v parametru zásad. |auditIfNotExists |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Guest%20Configuration/GuestConfiguration_AdministratorsGroupMembers_AINE.json) |
|[Auditovat počítače s Windows, které mají zadané členy ve skupině Administrators](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F69bf4abd-ca1e-4cf6-8b5a-762d42e61d4f) |Vyžaduje nasazení požadovaných požadavků do oboru přiřazení zásad. Podrobnosti najdete na adrese [https://aka.ms/gcpol](https://aka.ms/gcpol) . Počítače jsou nekompatibilní, pokud místní skupina Administrators obsahuje jednoho nebo více členů uvedených v parametru zásad. |auditIfNotExists |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Guest%20Configuration/GuestConfiguration_AdministratorsGroupMembersToExclude_AINE.json) |
