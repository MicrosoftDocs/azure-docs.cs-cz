---
title: Primární, cizí a jedinečné klíče
description: Omezení tabulky podporují používání vyhrazeného fondu SQL ve službě Azure synapse Analytics
services: synapse-analytics
author: mstehrani
manager: craigg
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql-dw
ms.date: 09/05/2019
ms.author: emtehran
ms.reviewer: nibruno; jrasnick
ms.custom: seo-lt-2019, azure-synapse
ms.openlocfilehash: 88b63ce30000340a70811e9f623e4273ccbb272a
ms.sourcegitcommit: aacbf77e4e40266e497b6073679642d97d110cda
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/12/2021
ms.locfileid: "98117278"
---
# <a name="primary-key-foreign-key-and-unique-key-using-dedicated-sql-pool-in-azure-synapse-analytics"></a>Primární klíč, cizí klíč a jedinečný klíč pomocí vyhrazeného fondu SQL ve službě Azure synapse Analytics

Přečtěte si o omezeních tabulek ve vyhrazeném fondu SQL, včetně primárního klíče, cizího klíče a jedinečného klíče.

## <a name="table-constraints"></a>Omezení tabulky

Vyhrazený fond SQL podporuje tato omezení tabulky: 
- PRIMÁRNÍ klíč se podporuje jenom v případě, že se používají jenom neclusterované a nevynucované.    
- JEDINEČNÉ omezení se podporuje jenom s nevynucovaném využitím.

Pro syntaxi můžete zaškrtnout možnost [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) and [Create Table](/sql/t-sql/statements/create-table-azure-sql-data-warehouse). 

Omezení CIZÍho klíče není ve vyhrazeném fondu SQL podporováno.  


## <a name="remarks"></a>Poznámky

S primárním klíčem a/nebo jedinečným klíčem umožňuje vyhrazený modul SQL poolu vygenerovat pro dotaz optimální plán spouštění.  Všechny hodnoty ve sloupci primárního klíče nebo ve sloupci jedinečné omezení by měly být jedinečné.

Po vytvoření tabulky s primárním klíčem nebo jedinečným omezením ve vyhrazeném fondu SQL musí uživatelé zajistit, aby všechny hodnoty v těchto sloupcích byly jedinečné.  Porušení, které by mohlo způsobit, že dotaz vrátí nepřesný výsledek.  Tento příklad ukazuje, jak může dotaz vracet nepřesný výsledek, pokud sloupec primárního klíče nebo jedinečné omezení obsahuje duplicitní hodnoty.  

```sql
 -- Create table t1
CREATE TABLE t1 (a1 INT NOT NULL, b1 INT) WITH (DISTRIBUTION = ROUND_ROBIN)

-- Insert values to table t1 with duplicate values in column a1.
INSERT INTO t1 VALUES (1, 100)
INSERT INTO t1 VALUES (1, 1000)
INSERT INTO t1 VALUES (2, 200)
INSERT INTO t1 VALUES (3, 300)
INSERT INTO t1 VALUES (4, 400)

-- Run this query.  No primary key or unique constraint.  4 rows returned. Correct result.
SELECT a1, COUNT(*) AS total FROM t1 GROUP BY a1

/*
a1          total
----------- -----------
1           2
2           1
3           1
4           1

(4 rows affected)
*/

-- Add unique constraint
ALTER TABLE t1 ADD CONSTRAINT unique_t1_a1 unique (a1) NOT ENFORCED

-- Re-run this query.  5 rows returned.  Incorrect result.
SELECT a1, count(*) AS total FROM t1 GROUP BY a1

/*
a1          total
----------- -----------
2           1
4           1
1           1
3           1
1           1

(5 rows affected)
*/

-- Drop unique constraint.
ALTER TABLE t1 DROP CONSTRAINT unique_t1_a1

-- Add primary key constraint
ALTER TABLE t1 add CONSTRAINT PK_t1_a1 PRIMARY KEY NONCLUSTERED (a1) NOT ENFORCED

-- Re-run this query.  5 rows returned.  Incorrect result.
SELECT a1, COUNT(*) AS total FROM t1 GROUP BY a1

/*
a1          total
----------- -----------
2           1
4           1
1           1
3           1
1           1

(5 rows affected)
*/

-- Manually fix the duplicate values in a1
UPDATE t1 SET a1 = 0 WHERE b1 = 1000

-- Verify no duplicate values in column a1 
SELECT * FROM t1

/*
a1          b1
----------- -----------
2           200
3           300
4           400
0           1000
1           100

(5 rows affected)
*/

-- Add unique constraint
ALTER TABLE t1 add CONSTRAINT unique_t1_a1 UNIQUE (a1) NOT ENFORCED  

-- Re-run this query.  5 rows returned.  Correct result.
SELECT a1, COUNT(*) as total FROM t1 GROUP BY a1

/*
a1          total
----------- -----------
2           1
3           1
4           1
0           1
1           1

(5 rows affected)
*/

-- Drop unique constraint.
ALTER TABLE t1 DROP CONSTRAINT unique_t1_a1

-- Add primary key contraint
ALTER TABLE t1 ADD CONSTRAINT PK_t1_a1 PRIMARY KEY NONCLUSTERED (a1) NOT ENFORCED

-- Re-run this query.  5 rows returned.  Correct result.
SELECT a1, COUNT(*) AS total FROM t1 GROUP BY a1

/*
a1          total
----------- -----------
2           1
3           1
4           1
0           1
1           1

(5 rows affected)
*/

```

## <a name="examples"></a>Příklady

Vytvořte vyhrazenou tabulku fondu SQL s primárním klíčem: 

```sql 
CREATE TABLE mytable (c1 INT PRIMARY KEY NONCLUSTERED NOT ENFORCED, c2 INT);
```

Vytvořte vyhrazenou tabulku fondu SQL s jedinečným omezením:

```sql
CREATE TABLE t6 (c1 INT UNIQUE NOT ENFORCED, c2 INT);
```

## <a name="next-steps"></a>Další kroky

Po vytvoření tabulek pro vyhrazený fond SQL je dalším krokem načtení dat do tabulky. Kurz načítání najdete v tématu [načtení dat do vyhrazeného fondu SQL](load-data-wideworldimportersdw.md).