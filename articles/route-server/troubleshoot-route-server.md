---
title: Řešení potíží s Azure Route serverem
description: Naučte se řešit problémy pro server Azure Route.
services: route-server
author: duongau
ms.service: route-server
ms.topic: how-to
ms.date: 03/15/2021
ms.author: duau
ms.openlocfilehash: 83f1e83653c5674988cadcb5b54d3c675ae0b8b8
ms.sourcegitcommit: 4bda786435578ec7d6d94c72ca8642ce47ac628a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2021
ms.locfileid: "103489436"
---
# <a name="troubleshooting-azure-route-server-issues"></a>Řešení potíží s Azure Route serverem

> [!IMPORTANT]
> Služba Azure Route Server (Preview) je aktuálně ve verzi Public Preview.
> Tato verze Preview se poskytuje bez smlouvy o úrovni služeb a nedoporučuje se pro úlohy v produkčním prostředí. Některé funkce se nemusí podporovat nebo mohou mít omezené možnosti.
> Další informace najdete v [dodatečných podmínkách použití pro verze Preview v Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="connectivity-issues"></a>Problémy s připojením

### <a name="why-does-my-nva-lose-internet-connectivity-after-it-advertises-the-default-route-00000-to-azure-route-server"></a>Proč můj síťové virtuální zařízení ztratí připojení k Internetu poté, co se inzeruje výchozí trasa (0.0.0.0/0) do serveru služby Azure Route?
Když váš síťové virtuální zařízení inzeruje výchozí trasu, server Azure Route je naprogramuje pro všechny virtuální počítače ve virtuální síti, včetně samotného síťové virtuální zařízení. Tato výchozí trasa nastaví síťové virtuální zařízení jako další segment směrování pro všechny přenosy vázané na Internet. Pokud vaše síťové virtuální zařízení potřebuje připojení k Internetu, je potřeba nakonfigurovat [trasu definovanou uživatelem](../virtual-network/virtual-networks-udr-overview.md) , aby přepsala tuto výchozí trasu z síťové virtuální zařízení, a připojit udr k podsíti, ve které je služba síťové virtuální zařízení hostovaná (viz následující příklad). V opačném případě hostitelský počítač síťové virtuální zařízení nadále posílá provoz vázaný na Internet, včetně toho, který odesílá síťové virtuální zařízení zpět do samotného síťové virtuální zařízení.

| Trasa | Další segment směrování |
|-------|----------|
| 0.0.0.0/0 | Internet |


### <a name="why-can-i-ping-from-my-nva-to-the-bgp-peer-ip-on-azure-route-server-but-after-i-set-up-the-bgp-peering-between-them-i-cant-ping-the-same-ip-anymore-why-does-the-bgp-peering-go-down"></a>Proč se dá provést příkaz k odeslání z síťové virtuální zařízení do IP adresy partnerského uzlu protokolu BGP na serveru Azure Route, ale po nastavení partnerského vztahu protokolu BGP mezi nimi Nemůžu Nemůžu testovat stejnou IP adresu? Proč se partnerský vztah protokolu BGP rozchází?

V některých síťové virtuální zařízení je potřeba přidat statickou trasu pro podsíť serveru Azure Route. Pokud je například Azure Route Server v 10.0.255.0/27 a vaše síťové virtuální zařízení je v 10.0.1.0/24, musíte do směrovací tabulky v síťové virtuální zařízení přidat následující trasu:

| Trasa | Další segment směrování |
|-------|----------|
| 10.0.255.0/27 | 10.0.1.1 |

10.0.1.1 je výchozí IP adresa brány v podsíti, ve které je hostovaný síťové virtuální zařízení (nebo přesněji jedna z síťových karet).

### <a name="why-do-i-lose-connectivity-to-my-on-premises-network-over-expressroute-andor-azure-vpn-when-im-deploying-azure-route-server-to-a-virtual-network-that-already-has-expressroute-gateway-andor-azure-vpn-gateway"></a>Proč se při nasazování serveru Azure Route do virtuální sítě, která už má ExpressRoute Gateway nebo Azure VPN Gateway, ztratí připojení k místní síti přes ExpressRoute a/nebo Azure VPN?
Když nasadíte Server Azure Route do virtuální sítě, musíme aktualizovat rovinu ovládacího prvku mezi bránami a virtuální sítí. Během této aktualizace dojde k časovému období, kdy virtuální počítače ve virtuální síti ztratí připojení k místní síti. Důrazně doporučujeme, abyste naplánovali údržbu nasazení serveru Směrování Azure v produkčním prostředí.  

## <a name="control-plane-issues"></a>Problémy s řízením roviny

### <a name="why-is-the-bgp-peering-between-my-nva-and-the-azure-route-server-going-up-and-down-flapping"></a>Proč se partnerský vztah protokolu BGP mezi síťové virtuální zařízení a serverem Azure Route prochází a vypíná ("přepíná")?

Příčinou přepíná může být nastavení časovače protokolu BGP. Ve výchozím nastavení je časovač Keep-Alive na serveru Azure Route nastavený na 60 sekund a časovač podržení je 180 sekund.

### <a name="why-does-my-nva-not-receive-routes-from-azure-route-server-even-though-the-bgp-peering-is-up"></a>Proč moje síťové virtuální zařízení nepřijímá trasy z Azure Route serveru i v případě, že je partnerský vztah protokolu BGP zapnutý?

ASN, kterou používá Azure Route Server, je 65515. Ujistěte se, že jste pro svůj síťové virtuální zařízení nakonfigurovali jiné číslo ASN, aby bylo možné navázat relaci "eBGP" mezi vaším síťové virtuální zařízení a serverem tras Azure, aby k šíření tras mohlo dojít automaticky. Ujistěte se, že ve své konfiguraci protokolu BGP povolíte "Multi-hop", protože váš síťové virtuální zařízení a směrovací server Azure jsou v různých podsítích ve virtuální síti.

### <a name="the-bgp-peering-between-my-nva-and-azure-route-server-is-up-i-can-see-routes-exchanged-correctly-between-them-why-arent-the-nva-routes-in-the-effective-routing-table-of-my-vm"></a>Partnerský vztah protokolu BGP mezi síťové virtuální zařízení a serverem Azure Route Server je. Vidíte, že mezi nimi byly vyměňovány trasy správně. Proč nejsou síťové virtuální zařízení trasy v efektivní tabulce směrování tohoto virtuálního počítače? 

* Pokud je váš virtuální počítač ve stejné virtuální síti jako síťové virtuální zařízení a server tras Azure:

     Azure Route Server zveřejňuje dvě IP adresy partnerského uzlu protokolu BGP, které jsou hostované na dvou virtuálních počítačích, které sdílejí zodpovědnost za odesílání tras do všech ostatních virtuálních počítačů spuštěných ve vaší virtuální síti. Každé z vašich síťové virtuální zařízení musí nastavovat dvě totožné relace protokolu BGP (například použít stejné číslo, stejné jako pro cestu a inzerovat stejnou sadu tras) pro dva virtuální počítače, aby virtuální počítače ve virtuální síti mohly získávat konzistentní informace o směrování z Azure Route serveru. Podívejte se na diagram níže.

    ![Diagram znázorňující síťové virtuální zařízení s směrovacím serverem.](./media/faq/network-virtual-appliances.png)

    Pokud máte dvě nebo více instancí síťové virtuální zařízení, *můžete* pro stejnou trasu z různých instancí síťové virtuální zařízení inzerovat jiné jako cesty, pokud chcete určit jednu instanci síťové virtuální zařízení jako aktivní a jinou pasivní.

* Pokud se virtuální počítač nachází v jiné virtuální síti než ta, která hostuje váš síťové virtuální zařízení a server Azure Route. Ověřte, jestli je mezi dvěma virtuální sítě povolená síť VNet peering *a* jestli je ve virtuální síti virtuálního počítače povolený vzdálený server směrování.

## <a name="next-steps"></a>Další kroky

Informace o tom, jak [nakonfigurovat server tras Azure](quickstart-configure-route-server-powershell.md)
