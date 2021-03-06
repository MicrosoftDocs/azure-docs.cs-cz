---
title: Kurz – přístup k privátnímu cloudu
description: Přečtěte si, jak získat přístup k privátnímu cloudu řešení Azure VMware.
ms.topic: tutorial
ms.date: 03/13/2021
ms.openlocfilehash: f2af1cffda08bf4b9c62e63f32d36cc9bbd7024a
ms.sourcegitcommit: 4bda786435578ec7d6d94c72ca8642ce47ac628a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2021
ms.locfileid: "103494389"
---
# <a name="tutorial-access-an-azure-vmware-solution-private-cloud"></a>Kurz: přístup k privátnímu cloudu řešení Azure VMware

Řešení Azure VMware vám neumožňuje spravovat váš privátní cloud pomocí místního serveru vCenter. Pomocí pole pro přechod se budete muset připojit k instanci vCenter řešení Azure VMware. 

V tomto kurzu vytvoříte v rámci skupiny prostředků, kterou jste vytvořili v [předchozím kurzu](tutorial-configure-networking.md) , pole s odkazem a přihlásíte se k Azure VMware Solution vCenter. Tento skokový rámeček je virtuální počítač s Windows ve stejné virtuální síti, kterou jste vytvořili.  Poskytuje přístup k vCenter i NSX Manageru. 

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvoření virtuálního počítače s Windows pro přístup k Azure VMware Solution vCenter
> * Přihlaste se k vCenter z tohoto virtuálního počítače.

## <a name="create-a-new-windows-virtual-machine"></a>Vytvoření nového virtuálního počítače s Windows

[!INCLUDE [create-avs-jump-box-steps](includes/create-jump-box-steps.md)]

## <a name="connect-to-the-local-vcenter-of-your-private-cloud"></a>Připojení k místnímu vCenter vašeho privátního cloudu

1. V poli pro skok se přihlaste k vSphere klientovi pomocí služby VMware vCenter SSO pomocí uživatelského jména správce cloudu a ověřte, že se uživatelské rozhraní úspěšně zobrazuje.

1. V Azure Portal vyberte svůj privátní cloud a pak **spravujte**  >  **identitu**. 

   Adresy URL a přihlašovací údaje uživatele pro zobrazení privátního cloudu vCenter a správce NSX-T.

   :::image type="content" source="media/tutorial-access-private-cloud/ss4-display-identity.png" alt-text="Zobrazí adresy URL a přihlašovací údaje privátního cloudu vCenter a NSX Manageru." border="true" lightbox="media/tutorial-access-private-cloud/ss4-display-identity.png":::

1. Přejděte na virtuální počítač, který jste vytvořili v předchozím kroku, a připojte se k virtuálnímu počítači. 

   Pokud potřebujete pomáhat s připojením k VIRTUÁLNÍmu počítači, přečtěte si podrobnosti v tématu [připojení k virtuálnímu počítači](../virtual-machines/windows/connect-logon.md#connect-to-the-virtual-machine) .

1. Na virtuálním počítači s Windows otevřete prohlížeč a přejděte na adresu URL správce vCenter a NSX-T na dvou kartách. 

1. Na kartě vCenter zadejte `cloudadmin@vmcp.local` přihlašovací údaje uživatele z předchozího kroku.

   :::image type="content" source="media/tutorial-access-private-cloud/ss5-vcenter-login.png" alt-text="Přihlaste se k privátnímu cloudu vCenter." border="true":::

   :::image type="content" source="media/tutorial-access-private-cloud/ss6-vsphere-client-home.png" alt-text="portál vCenter." border="true":::

1. Na druhé kartě prohlížeče se přihlaste ke Správci NSX-T.

   :::image type="content" source="media/tutorial-access-private-cloud/ss10-nsx-manager-home.png" alt-text="Na druhé kartě prohlížeče se přihlaste ke Správci NSX-T." border="true":::



## <a name="next-steps"></a>Další kroky

V tomto kurzu jste se naučili:

> [!div class="checklist"]
> * Vytvořit virtuální počítač s Windows, který se má použít pro připojení k serveru vCenter
> * Přihlaste se k vCenter z virtuálního počítače.

Přejděte k dalšímu kurzu, kde se dozvíte, jak vytvořit virtuální síť pro nastavení místní správy pro clustery privátních cloudů.

> [!div class="nextstepaction"]
> [Vytvoření Virtual Network](tutorial-configure-networking.md)


