---
title: VÝKON v Azure Cosmos DB dotazovací jazyk
description: Přečtěte si o výkonu funkcí systému SQL v Azure Cosmos DB.
author: ginamr
ms.service: cosmos-db
ms.subservice: cosmosdb-sql
ms.topic: conceptual
ms.date: 09/13/2019
ms.author: girobins
ms.custom: query-reference
ms.openlocfilehash: 39db52223feea63a4e3afbd4775f884acbbca548
ms.sourcegitcommit: fa90cd55e341c8201e3789df4cd8bd6fe7c809a3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/04/2020
ms.locfileid: "93341684"
---
# <a name="power-azure-cosmos-db"></a>NAPÁJENÍ (Azure Cosmos DB)
[!INCLUDE[appliesto-sql-api](includes/appliesto-sql-api.md)]

 Vrátí hodnotu zadaného výrazu zadané mocniny.  
  
## <a name="syntax"></a>Syntaxe
  
```sql
POWER (<numeric_expr1>, <numeric_expr2>)  
```  
  
## <a name="arguments"></a>Argumenty
  
*numeric_expr1*  
   Je numerický výraz.  
  
*numeric_expr2*  
   Je mocninou, kterou chcete vyvolat *numeric_expr1*.  
  
## <a name="return-types"></a>Návratové typy
  
  Vrátí číselný výraz.  
  
## <a name="examples"></a>Příklady
  
  Následující příklad ukazuje vyvolání čísla mocninou čísla 3 (datová krychle čísla).  
  
```sql
SELECT POWER(2, 3) AS pow1, POWER(2.5, 3) AS pow2  
```  
  
 Zde je sada výsledků.  
  
```json
[{pow1: 8, pow2: 15.625}]  
```  

## <a name="next-steps"></a>Další kroky

- [Matematické funkce Azure Cosmos DB](sql-query-mathematical-functions.md)
- [Systémové funkce Azure Cosmos DB](sql-query-system-functions.md)
- [Úvod do služby Azure Cosmos DB](introduction.md)
