---
title: Co je Azure Route Server (Preview)?
description: Přečtěte si, jak může Azure Route Server zjednodušit směrování mezi virtuálním síťovým zařízením (síťové virtuální zařízení) a vaší virtuální sítí.
services: route-server
author: duongau
ms.service: route-server
ms.topic: overview
ms.date: 03/02/2021
ms.author: duau
ms.openlocfilehash: d868c064b96f58ab3febc1fd3b7f20b74d507cb0
ms.sourcegitcommit: 5bbc00673bd5b86b1ab2b7a31a4b4b066087e8ed
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/07/2021
ms.locfileid: "102437157"
---
# <a name="what-is-azure-route-server-preview"></a>Co je Azure Route Server (Preview)? 

Azure Route Server zjednodušuje dynamické směrování mezi virtuálním síťovým zařízením (síťové virtuální zařízení) a vaší virtuální sítí. Umožňuje výměnu informací o směrování přímo prostřednictvím protokolu BGP (Border Gateway Protocol) směrování mezi všemi síťové virtuální zařízení, které podporují směrovací protokol BGP a softwarově definované sítě (SDN) v Azure Virtual Network (VNET) bez nutnosti ruční konfigurace nebo údržby směrovacích tabulek. Azure Route Server je plně spravovaná služba a má nakonfigurovanou vysokou dostupnost.

> [!IMPORTANT]
> Služba Azure Route Server (Preview) je aktuálně ve verzi Public Preview.
> Tato verze Preview se poskytuje bez smlouvy o úrovni služeb a nedoporučuje se pro úlohy v produkčním prostředí. Některé funkce se nemusí podporovat nebo mohou mít omezené možnosti.
> Další informace najdete v [dodatečných podmínkách použití pro verze Preview v Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="how-does-it-work"></a>Jak to funguje?

Následující diagram znázorňuje, jak funguje server Azure Route s SDWAN síťové virtuální zařízení a síťové virtuální zařízení zabezpečení ve virtuální síti. Po navázání partnerského vztahu protokolu BGP dostane Azure Route Server místní trasu (10.250.0.0/16) ze zařízení SDWAN a výchozí trasou (0.0.0.0/0) z brány firewall. Tyto trasy se pak automaticky nakonfigurují na virtuálních počítačích ve virtuální síti. V důsledku toho se veškerý provoz směřující do místní sítě pošle do zařízení SDWAN. Všechny přenosy vázané na Internet budou odeslány do brány firewall. V opačném směru odešle server trase Azure adresu virtuální sítě (10.1.0.0/16) do obou síťová virtuální zařízení. Zařízení SDWAN ho může rozšířit do místní sítě.

![Diagram znázorňující, že je server Azure Route nakonfigurovaný ve virtuální síti.](./media/overview/route-server-overview.png)

## <a name="key-benefits"></a>Klíčové výhody 

Azure Route Server zjednodušuje konfiguraci, správu a nasazení vašich síťové virtuální zařízení ve vaší virtuální síti.  

* Nemusíte už ručně aktualizovat směrovací tabulku v síťové virtuální zařízení vždy, když se aktualizují adresy vaší virtuální sítě. 

* [Trasy definované uživatelem](../virtual-network/virtual-networks-udr-overview.md) už nemusíte ručně aktualizovat, kdykoli síťové virtuální zařízení oznamuje nové trasy nebo odejmou staré. 

* S využitím služby Azure Route Server můžete vytvořit partnerský vztah více instancí síťové virtuální zařízení. V síťové virtuální zařízení můžete nakonfigurovat atributy protokolu BGP a v závislosti na návrhu (například aktivní – aktivní pro výkon nebo aktivní – pasivní pro odolnost) Povolit službě Azure Route Server, která instance síťové virtuální zařízení je aktivní, nebo která je pasivní. 

* Rozhraní mezi síťové virtuální zařízení a serverem Azure Route je založené na společném standardním protokolu. Pokud váš síťové virtuální zařízení podporuje protokol BGP, můžete ho navázat na server Azure Route. Další informace najdete v tématu [podporované směrovací protokoly pro server tras](route-server-faq.md#protocol).

* Směrovací server Azure můžete nasadit v jakékoli nové nebo existující virtuální síti. 

## <a name="faq"></a>Časté otázky

Nejčastější dotazy týkající se Azure Route serveru najdete v tématu [Nejčastější dotazy k Azure Route serveru](route-server-faq.md).

## <a name="next-steps"></a>Další kroky

- [Informace o tom, jak nakonfigurovat server směrování Azure](quickstart-configure-route-server-powershell.md)
- [Přečtěte si, jak Azure Route server funguje se službou Azure ExpressRoute a Azure VPN.](expressroute-vpn-support.md)
