---
title: Automatické zvětšování úložiště – Azure CLI – Azure Database for MariaDB
description: Tento článek popisuje, jak můžete povolit automatické zvětšování úložiště pomocí rozhraní příkazového řádku Azure v Azure Database for MariaDB.
author: ambhatna
ms.author: ambhatna
ms.service: jroth
ms.topic: how-to
ms.date: 3/18/2020
ms.custom: devx-track-azurecli
ms.openlocfilehash: ba997038842a1028b8be5a542adac60186a30cb0
ms.sourcegitcommit: 52e3d220565c4059176742fcacc17e857c9cdd02
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/21/2021
ms.locfileid: "98664431"
---
# <a name="auto-grow-azure-database-for-mariadb-storage-using-the-azure-cli"></a>Automatické zvětšování Azure Database for MariaDBho úložiště pomocí Azure CLI
Tento článek popisuje, jak můžete nakonfigurovat úložiště serveru Azure Database for MariaDB pro růst, aniž by to ovlivnilo zatížení.

Server, který [dosáhl limitu úložiště](concepts-pricing-tiers.md#reaching-the-storage-limit), je nastaven na hodnotu jen pro čtení. Pokud je pro servery s méně než 100 GB zřízené úložiště povolené automatické zvětšování úložiště, velikost zřízeného úložiště se zvýší o 5 GB, jakmile bude volné úložiště nižší než 1 GB nebo 10% zřízené úložiště. U serverů s více než 100 GB zřízeného úložiště se velikost zřízeného úložiště zvyšuje o 5%, pokud je volný prostor úložiště pod 5% velikosti zřízeného úložiště. Maximální limity úložiště, jak je uvedeno [zde](concepts-pricing-tiers.md#storage) , platí.

## <a name="prerequisites"></a>Požadavky

Postup dokončení této příručky:

- Potřebujete [server Azure Database for MariaDB](quickstart-create-mariadb-server-database-using-azure-cli.md).

[!INCLUDE [azure-cli-prepare-your-environment-no-header.md](../../includes/azure-cli-prepare-your-environment-no-header.md)]

- Tento článek vyžaduje Azure CLI verze 2,0 nebo novější. Pokud používáte Azure Cloud Shell, nejnovější verze je už nainstalovaná.

## <a name="enable-mariadb-server-storage-auto-grow"></a>Povolit automatické zvětšování úložiště serveru MariaDB

Pomocí následujícího příkazu Povolte automatické zvětšení úložiště na stávajícím serveru:

```azurecli-interactive
az mariadb server update --name mydemoserver --resource-group myresourcegroup --auto-grow Enabled
```

Při vytváření nového serveru pomocí následujícího příkazu Povolte automatické zvětšování úložiště serveru:

```azurecli-interactive
az mariadb server create --resource-group myresourcegroup --name mydemoserver  --auto-grow Enabled --location westus --admin-user myadmin --admin-password <server_admin_password> --sku-name GP_Gen5_2 --version 10.3
```

## <a name="next-steps"></a>Další kroky

Přečtěte si informace o [tom, jak vytvářet výstrahy na metrikách](howto-alert-metric.md).
