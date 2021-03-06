---
title: Změna oznámení inteligentního zjišťování – Azure Application Insights
description: Přejděte na výchozí příjemce oznámení z inteligentního zjišťování. Inteligentní zjišťování umožňuje monitorovat trasování aplikací pomocí Azure Application Insights pro neobvyklé vzory v telemetrie trasování.
ms.topic: conceptual
author: harelbr
ms.author: harelbr
ms.date: 02/14/2021
ms.reviewer: mbullwin
ms.openlocfilehash: fa14f0dd40a30a4750d9bb102d8e67608f958135
ms.sourcegitcommit: c27a20b278f2ac758447418ea4c8c61e27927d6a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/03/2021
ms.locfileid: "101734498"
---
# <a name="smart-detection-e-mail-notification-change"></a>Změna e-mailových oznámení inteligentního zjišťování

Na základě zpětné vazby od zákazníků od 1. dubna 2019 měníme výchozí role, které přijímají e-mailová oznámení od inteligentního zjišťování.

## <a name="what-is-changing"></a>Co se mění?

V současné době se e-mailová oznámení inteligentní detekce standardně odesílají do rolí _vlastník_ předplatného, _přispěvatele_ předplatného a _modulu pro čtení předplatného_ Tyto role často zahrnují uživatele, kteří nejsou aktivně zapojeni do monitorování, což způsobí, že mnohé z těchto uživatelů dostanou oznámení zbytečně. Pro zlepšení tohoto prostředí provádíme změnu, aby e-mailová oznámení ve výchozím nastavení přešla jenom na role [Čtenář monitorování](../../role-based-access-control/built-in-roles.md#monitoring-reader) a [sledování](../../role-based-access-control/built-in-roles.md#monitoring-contributor) .

## <a name="scope-of-this-change"></a>Rozsah této změny

Tato změna bude mít vliv na všechna pravidla inteligentního zjišťování, s výjimkou následujících:

* Pravidla inteligentního zjišťování označená jako náhled Tato pravidla inteligentního zjišťování nepodporují e-mailová oznámení ještě dnes.

* Pravidlo anomálií selhání.

## <a name="how-to-prepare-for-this-change"></a>Jak připravit tuto změnu?

Aby bylo zajištěno, že budou pro příslušné uživatele zasílána e-mailová oznámení od inteligentního zjišťování, musí být uživatelé přiřazeni ke službě [Sledování monitorování](../../role-based-access-control/built-in-roles.md#monitoring-reader) nebo k rolím [přispěvatele](../../role-based-access-control/built-in-roles.md#monitoring-contributor) v předplatném.

Pokud chcete přiřazovat uživatele k rolím přispěvatele monitorování nebo monitorování pomocí Azure Portal, postupujte podle kroků popsaných v článku [přiřazení rolí Azure](../../role-based-access-control/role-assignments-portal.md) . Ujistěte se, že jste jako roli, ke které jsou přiřazeni uživatelé, vybrali možnost _Čtenář monitorování_ nebo _Přispěvatel monitorování_ .

> [!NOTE]
> Tato změna nebude mít vliv na konkrétní příjemce oznámení inteligentní detekce nakonfigurovaných pomocí možnosti _Další příjemci e-mailu_ v nastavení pravidla. Tito příjemci budou dál dostávat e-mailová oznámení.

Pokud máte nějaké dotazy nebo obavy týkající se této změny, váhají [nás kontaktujte](mailto:smart-alert-feedback@microsoft.com).

## <a name="next-steps"></a>Další kroky

Další informace o inteligentní detekci:

- [Anomálie selhání](./proactive-failure-diagnostics.md)
- [Nevracení paměti](./proactive-potential-memory-leak.md)
- [Anomálie výkonu](./proactive-performance-diagnostics.md)

