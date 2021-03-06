---
title: Použití sdílených imagí virtuálních počítačů k vytvoření sady škálování v Azure CLI
description: Naučte se používat rozhraní příkazového řádku Azure CLI k vytváření sdílených imagí virtuálních počítačů, které se použijí pro nasazení služby Virtual Machine Scale Sets v Azure.
author: axayjo
tags: azure-resource-manager
ms.service: virtual-machine-scale-sets
ms.subservice: imaging
ms.topic: conceptual
ms.date: 05/06/2019
ms.author: akjosh
ms.reviewer: cynthn
ms.custom: ''
ms.openlocfilehash: 418258c498f768697aefebd5df0cc64b7255076f
ms.sourcegitcommit: b39cf769ce8e2eb7ea74cfdac6759a17a048b331
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2021
ms.locfileid: "98676074"
---
# <a name="create-and-use-shared-images-for-virtual-machine-scale-sets-with-the-azure-cli-20"></a>Vytvoření a použití sdílených imagí pro Virtual Machine Scale Sets pomocí Azure CLI 2,0

Při vytváření škálovací sady zadáte image, která se použije při nasazení instancí virtuálních počítačů. [Galerie sdílených imagí](../virtual-machines/shared-image-galleries.md) zjednodušuje sdílení vlastních imagí v rámci vaší organizace. Vlastní image jsou podobné imagím z marketplace, ale vytváříte je sami. Vlastní image se dají použít ke spouštění konfigurací, jako jsou předběžné načítání aplikací, konfigurace aplikací a další konfigurace operačního systému. 

Galerie sdílených imagí umožňuje sdílet obrázky s ostatními. Vyberte, které Image chcete sdílet, které oblasti mají být v nástroji dostupné a které chcete sdílet s. 


[!INCLUDE [virtual-machines-common-shared-images-cli](../../includes/virtual-machines-common-shared-images-cli.md)]


## <a name="next-steps"></a>Další kroky

Vytvořte verzi image z [virtuálního počítače](../virtual-machines/image-version-vm-cli.md)nebo [spravované image](../virtual-machines/image-version-managed-image-cli.md).

Další informace o galeriích sdílených imagí najdete v [přehledu](../virtual-machines/shared-image-galleries.md). Pokud narazíte na problémy, přečtěte si téma [řešení potíží s galeriemi sdílených imagí](../virtual-machines/troubleshooting-shared-images.md).