---
title: Restart serveru – Azure PowerShell-Azure Database for PostgreSQL
description: Tento článek popisuje, jak můžete restartovat server Azure Database for PostgreSQL pomocí prostředí PowerShell.
author: lfittl-msft
ms.author: lufittl
ms.service: postgresql
ms.topic: how-to
ms.date: 06/08/2020
ms.custom: devx-track-azurepowershell
ms.openlocfilehash: 2d37de4a1861cb78b4a76c8ca7bc8c3643245b32
ms.sourcegitcommit: 0830e02635d2f240aae2667b947487db01f5fdef
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/21/2020
ms.locfileid: "97706962"
---
# <a name="restart-azure-database-for-postgresql-server-using-powershell"></a>Restartování serveru Azure Database for PostgreSQL pomocí prostředí PowerShell

Toto téma popisuje, jak můžete restartovat server Azure Database for PostgreSQL. Možná budete muset restartovat server z důvodů údržby, což způsobí krátkou výpadky během operace.

Pokud je služba zaneprázdněná, je restartování serveru blokované. Například služba může zpracovávat dříve požadovanou operaci, jako je například škálování virtuální jádra.

> [!NOTE] 
> Čas potřebný k dokončení restartování závisí na procesu obnovení PostgreSQL. Chcete-li zkrátit dobu restartování, doporučujeme, abyste minimalizovali množství aktivity, ke kterým došlo na serveru před restartováním. Můžete taky chtít zvýšit frekvenci kontrolního bodu. Můžete také ladit hodnoty parametrů souvisejících s kontrolními body `max_wal_size` , včetně. Doporučuje se také spustit `CHECKPOINT` příkaz před restartováním serveru.

## <a name="prerequisites"></a>Požadavky

K dokončení tohoto průvodce budete potřebovat:

- [Modul AZ PowerShell](/powershell/azure/install-az-ps) nainstalovaný místně nebo [Azure Cloud Shell](https://shell.azure.com/) v prohlížeči
- [Server Azure Database for PostgreSQL](quickstart-create-postgresql-server-database-using-azure-powershell.md)

> [!IMPORTANT]
> I když je modul PowerShell AZ. PostgreSql ve verzi Preview, musíte ho nainstalovat samostatně z modulu AZ PowerShellu pomocí následujícího příkazu: `Install-Module -Name Az.PostgreSql -AllowPrerelease` .
> Jakmile je modul PowerShellu AZ. PostgreSql všeobecně dostupný, bude součástí budoucna k tomu, aby vydaná vydání modulu PowerShellu a nativně dostupná v rámci Azure Cloud Shell.

Pokud se rozhodnete použít prostředí PowerShell místně, připojte se k účtu Azure pomocí rutiny [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount) .

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="restart-the-server"></a>Restartování serveru

Restartujte server pomocí následujícího příkazu:

```azurepowershell-interactive
Restart-AzPostgreSqlServer -Name mydemoserver -ResourceGroupName myresourcegroup
```

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Vytvoření serveru Azure Database for PostgreSQL pomocí prostředí PowerShell](quickstart-create-postgresql-server-database-using-azure-powershell.md)