---
title: Zobrazit podrobnosti o ověřování Azure Maps
description: Pomocí Azure Portal můžete zobrazit podrobnosti o ověřování Azure Maps.
author: anastasia-ms
ms.author: v-stharr
ms.date: 06/17/2020
ms.topic: include
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.openlocfilehash: a6ffcbf5a8c36958dd3ea74de4d826fe25a1139c
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/09/2020
ms.locfileid: "87126447"
---
Podrobnosti o ověřování účtu Azure Maps můžete zobrazit v Azure Portal. Ve svém účtu v nabídce **Nastavení** vyberte **ověřování**.

![Podrobnosti ověřování](../media/how-to-manage-authentication/how-to-view-auth.png)

Po vytvoření účtu Azure Maps se hodnota Azure Maps nachází na `x-ms-client-id` stránce s podrobnostmi ověřování Azure Portal. Tato hodnota představuje účet, který se bude používat pro REST API požadavky. Tato hodnota by měla být uložena v konfiguraci aplikace a načtena před provedením požadavků HTTP při použití ověřování Azure AD s Azure Maps.
