---
title: Řešení potíží s replikací mezi oblastmi Azure NetApp Files | Microsoft Docs
description: Popisuje chybové zprávy a řešení, které vám můžou pomoct při řešení potíží s replikací mezi jednotlivými oblastmi Azure NetApp Files.
services: azure-netapp-files
documentationcenter: ''
author: b-juche
manager: ''
editor: ''
ms.assetid: ''
ms.service: azure-netapp-files
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 11/18/2020
ms.author: b-juche
ms.openlocfilehash: b30ed0cca680013b85efe064d59fb7cb73d753d2
ms.sourcegitcommit: 30906a33111621bc7b9b245a9a2ab2e33310f33f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/22/2020
ms.locfileid: "95239546"
---
# <a name="troubleshoot-cross-region-replication"></a>Řešení potíží s replikací mezi oblastmi

Tento článek popisuje chybové zprávy a řešení, které vám můžou pomoct vyřešit problémy s replikací mezi jednotlivými oblastmi Azure NetApp Files. 

## <a name="errors-creating-replication"></a>Chyby při vytváření replikace  

|     Chybová zpráva    |     Řešení    |
|-|-|
|     `Volume {0} cannot   be used as source because it is already in replication`    |     Nejde vytvořit replikaci se zdrojovým svazkem, který už je v relaci replikace dat.    |
|     `Peered region   '{0}' is not accepted`    |     Pokoušíte se vytvořit replikaci mezi nepartnerskými oblastmi.    |
|     `RemoteVolumeResource   '{0}' of wrong type '{1}'`    |     Ověřte, že ID vzdáleného prostředku je ID prostředku svazku.    |

## <a name="errors-authorizing-volume"></a>Chyby při autorizaci svazku  

|     Chybová zpráva    |     Řešení    |
|-|-|
|     `Missing value   for 'AuthorizeSourceReplication'`    |     `RemoteResourceID`Chybí nebo je neplatný v uživatelském rozhraní nebo požadavku rozhraní API (oprava chybové zprávy).    |
|     `Missing value   for 'RemoteVolumeResourceId'`    |     V   `RemoteResourceID` uživatelském rozhraní nebo v požadavku rozhraní API chybí nebo není platný.    |
|     `Data   Protection volume not found for RemoteVolumeResourceId: {remoteResourceId}`    |     Ověřte, jestli   `RemoteResourceID` je pro uživatele správná, nebo jestli existuje.    |
|     `Remote volume   '{0}' is not configured for replication`    |     Cílový svazek není svazek ochrany dat.    |
|     `Remote volume   '{0}' does not have source volume '{1}' as RemoteVolumeResourceId`    |     Svazek ochrany dat nemá tento zdrojový svazek ve svém ID vzdáleného prostředku (bylo zadáno chybné ID zdroje).    |
|     `The   destination volume replication creation failed (message: {0})`    |     Tato chyba indikuje chybu serveru. Obraťte se na podporu.    |

## <a name="errors-deleting-replication"></a>Chyby při odstraňování replikace

|     Chybová zpráva    |     Řešení    |
|-|-|
|     `Replication   cannot be deleted, mirror state needs to be in status: Broken before deleting`    |     Ověřte, že buď byla replikace přerušená, nebo není inicializovaná a nečinná (inicializace se nezdařila).    |
|     `Cannot delete   source replication`    |     Odstranění replikace ze strany zdroje není povoleno. Ujistěte se, že odstraňujete replikaci z cílové strany.    |

## <a name="errors-deleting-volume"></a>Chyby při odstraňování svazku

|     Chybová zpráva    |     Řešení    |
|-|-|
| `Volume is a member of an active volume replication relationship`  |  Před odstraněním svazku odstraňte replikaci. Viz [odstranění replikace](cross-region-replication-delete.md). Tato operace vyžaduje, abyste před odstraněním replikace svazku přerušili vytváření partnerských vztahů. |
| `Volume with replication cannot be deleted`  |  Před odstraněním svazku odstraňte replikaci. Viz [odstranění replikace](cross-region-replication-delete.md). Tato operace vyžaduje, abyste před odstraněním replikace svazku přerušili vytváření partnerských vztahů. 

## <a name="errors-resyncing-volume"></a>Chyby při opětovné synchronizaci svazku

|     Chybová zpráva    |     Řešení    |
|-|-|
|     `Volume Replication is in invalid status: (Mirrored|Uninitialized) for operation: 'ResyncReplication'`     |     Ověřte, zda je replikace svazku ve stavu "přerušeno".    |

## <a name="errors-deleting-snapshot"></a>Chyby při odstraňování snímku 

|     Chybová zpráva    |     Řešení    |
|-|-|
|     `Snapshot   cannot be deleted, parent volume is a Data Protection volume with a   replication object`    |     Pokud chcete tento snímek odstranit, ověřte, jestli jste přerušili replikaci svazku.    |
|     `Cannot delete   volume replication generated snapshot`    |     Odstranění snímků směrného plánu replikace se nepovoluje.    |

## <a name="next-steps"></a>Další kroky  

* [Replikace mezi oblastmi](cross-region-replication-introduction.md)
* [Požadavky a předpoklady pro použití replikace mezi oblastmi](cross-region-replication-requirements-considerations.md)
* [Vytvoření replikace svazků](cross-region-replication-create-peering.md)
* [Zobrazení stavu vztahu replikace](cross-region-replication-display-health-status.md)
* [Správa zotavení po havárii](cross-region-replication-manage-disaster-recovery.md)
* [Řešení potíží s replikací mezi oblastmi](troubleshoot-cross-region-replication.md)
