---
title: Vytvoření svazku SMB pro Azure NetApp Files | Microsoft Docs
description: V tomto článku se dozvíte, jak vytvořit SMB3 svazek v Azure NetApp Files. Seznamte se s požadavky na připojení služby Active Directory a doménové služby.
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
ms.topic: how-to
ms.date: 02/16/2021
ms.author: b-juche
ms.openlocfilehash: 91f4f90658281282cdcb01b091bd9c9647d8d702
ms.sourcegitcommit: 58ff80474cd8b3b30b0e29be78b8bf559ab0caa1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/17/2021
ms.locfileid: "100635481"
---
# <a name="create-an-smb-volume-for-azure-netapp-files"></a>Vytvoření svazku SMB pro Azure NetApp Files

Azure NetApp Files podporuje vytváření svazků pomocí systému souborů NFS (NFSv3 a NFSv 4.1), SMB3 nebo duálního protokolu (NFSv3 a SMB). Spotřeba kapacity svazku se počítá proti zřízené kapacitě příslušného fondu. V tomto článku se dozvíte, jak vytvořit svazek SMB3.

## <a name="before-you-begin"></a>Než začnete 

* Musíte mít už nastavený fond kapacity. Viz [nastavení fondu kapacit](azure-netapp-files-set-up-capacity-pool.md).     
* Podsíť musí být delegovaná na Azure NetApp Files. Viz [delegování podsítě na Azure NetApp Files](azure-netapp-files-delegate-subnet.md).

## <a name="configure-active-directory-connections"></a>Konfigurace připojení ke službě Active Directory 

Před vytvořením svazku SMB je potřeba vytvořit připojení ke službě Active Directory. Pokud jste nenakonfigurovali připojení služby Active Directory pro soubory Azure NetApp, postupujte podle pokynů uvedených v tématu [Vytvoření a Správa připojení ke službě Active Directory](create-active-directory-connections.md).

## <a name="add-an-smb-volume"></a>Přidat svazek SMB

1. V okně fondy kapacit klikněte na okno **svazky** . 

    ![Přejít na svazky](../media/azure-netapp-files/azure-netapp-files-navigate-to-volumes.png)

2. Kliknutím na **+ Přidat svazek** vytvořte svazek.  
    Zobrazí se okno vytvořit svazek.

3. V okně vytvořit svazek klikněte na **vytvořit** a zadejte informace pro následující pole na kartě základy:   
    * **Název svazku**      
        Zadejte název svazku, který vytváříte.   

        Název svazku musí být v rámci každého fondu kapacity jedinečný. Musí mít aspoň tři znaky dlouhé. Můžete použít jakékoli alfanumerické znaky.   

        Nemůžete použít `default` nebo `bin` jako název svazku.

    * **Fond kapacit**  
        Zadejte fond kapacit, ve kterém chcete vytvořit svazek.

    * **Kvóta**  
        Určuje velikost logického úložiště, které je přidělené svazku.  

        Pole **Dostupná kvóta** zobrazuje množství nevyužitého místa ve zvoleném fondu kapacity, které můžete použít k vytvoření nového svazku. Velikost nového svazku nesmí překročit dostupnou kvótu.  

    * **Propustnost (MiB/S)**   
        Pokud je svazek vytvořený v manuálním fondu kapacity QoS, určete propustnost, kterou pro svazek požadujete.   

        Pokud se svazek vytvoří ve fondu kapacity auto QoS, hodnota zobrazená v tomto poli je (propustnost × úroveň služby).   

    * **Virtuální síť**  
        Zadejte službu Azure Virtual Network (VNet), ze které chcete získat přístup ke svazku.  

        Virtuální síť, kterou zadáte, musí mít přidělenou podsíť Azure NetApp Files. Služba Azure NetApp Files se dá použít jenom ze stejné virtuální sítě nebo z virtuální sítě, která se nachází ve stejné oblasti jako svazek prostřednictvím partnerského vztahu virtuálních sítí. Ke svazku z místní sítě se můžete dostat i přes Express Route.   

    * **Podsíť**  
        Zadejte podsíť, kterou chcete použít pro svazek.  
        Podsíť, kterou zadáte, musí být delegovaná na Azure NetApp Files. 
        
        Pokud jste nedelegovanou podsíť, můžete na stránce vytvořit svazek kliknout na **vytvořit novou** . Pak na stránce vytvořit podsíť zadejte informace o podsíti a vyberte možnost **Microsoft. NetApp/** Volumes pro delegování podsítě pro Azure NetApp Files. V každé virtuální síti je možné delegovat jenom jednu podsíť na Azure NetApp Files.   
 
        ![Vytvoření svazku](../media/azure-netapp-files/azure-netapp-files-new-volume.png)
    
        ![Vytvoření podsítě](../media/azure-netapp-files/azure-netapp-files-create-subnet.png)

    * Pokud chcete pro svazek použít existující zásadu snímku, rozbalte ji kliknutím na **Zobrazit Upřesnit oddíl** , určete, jestli chcete cestu k snímku skrýt, a v rozevírací nabídce vyberte zásadu snímku. 

        Informace o vytváření zásad snímku najdete v tématu [Správa zásad snímků](azure-netapp-files-manage-snapshots.md#manage-snapshot-policies).

        ![Zobrazit rozšířený výběr](../media/azure-netapp-files/volume-create-advanced-selection.png)

4. Klikněte na **protokol** a vyplňte následující informace:  
    * Jako typ protokolu pro svazek vyberte **SMB** . 
    * V rozevíracím seznamu vyberte připojení ke **službě Active Directory** .
    * Zadejte název sdíleného svazku do pole  **název sdílené složky**.

    ![Zadat protokol SMB](../media/azure-netapp-files/azure-netapp-files-protocol-smb.png)

5. Kliknutím na tlačítko **zkontrolovat + vytvořit** zkontrolujte podrobnosti o svazku.  Pak kliknutím na **vytvořit** vytvořte svazek SMB.

    Svazek, který jste vytvořili, se zobrazí na stránce svazky. 
 
    Svazek dědí atributy předplatného, skupiny prostředků a umístění z fondu kapacity. Stav nasazení svazku můžete monitorovat na kartě Oznámení.

## <a name="control-access-to-an-smb-volume"></a>Řízení přístupu ke svazku SMB  

Přístup ke svazku SMB je spravovaný prostřednictvím oprávnění.  

### <a name="share-permissions"></a>Oprávnění ke sdílení  

Ve výchozím nastavení má nový svazek oprávnění ke sdílení **všech uživatelů a úplné řízení** . Členové skupiny Domain Admins mohou změnit oprávnění ke sdílení pomocí správy počítače v účtu počítače, který se používá pro Azure NetApp Files svazek.

![](../media/azure-netapp-files/smb-mount-path.png) 
 ![ Oprávnění k nastavení sdílené složky pro cestu pro připojení SMB](../media/azure-netapp-files/set-share-permissions.png) 

### <a name="ntfs-file-and-folder-permissions"></a>Oprávnění k souborům a složkám NTFS  

Oprávnění pro soubor nebo složku můžete nastavit pomocí karty **zabezpečení** vlastností objektu v klientovi Windows SMB.
 
![Nastavení oprávnění k souborům a složkám](../media/azure-netapp-files/set-file-folder-permissions.png) 

## <a name="next-steps"></a>Další kroky  

* [Připojení nebo odpojení svazku pro virtuální počítače s Windows nebo Linuxem](azure-netapp-files-mount-unmount-volumes-for-virtual-machines.md)
* [Omezení prostředků pro službu Azure NetApp Files](azure-netapp-files-resource-limits.md)
* [Nejčastější dotazy k protokolu SMB](./azure-netapp-files-faqs.md#smb-faqs)
* [Řešení potíží se svazky SMB nebo Dual-Protocol](troubleshoot-dual-protocol-volumes.md)
* [Informace o integraci virtuální sítě pro služby Azure](../virtual-network/virtual-network-for-azure-services.md)
* [Instalace nové doménové struktury služby Active Directory pomocí Azure CLI](/windows-server/identity/ad-ds/deploy/virtual-dc/adds-on-azure-vm)
