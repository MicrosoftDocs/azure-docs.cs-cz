---
author: v-dalc
ms.service: databox
ms.author: alkohli
ms.topic: include
ms.date: 03/02/2021
ms.openlocfilehash: 57415ec76a3e8d9fc3c160b47668d3419ff6ea5c
ms.sourcegitcommit: 18a91f7fe1432ee09efafd5bd29a181e038cee05
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2021
ms.locfileid: "103622292"
---
K řešení chyb souvisejících s výpočty použijte IoT Edge odezvy agenta modulu runtime. Tady je seznam možných odpovědí:

* 200 – OK
* 400 – konfigurace nasazení je poškozená nebo neplatná.
* 417 – zařízení nemá nastavenou konfiguraci nasazení.
* 412 – verze schématu v konfiguraci nasazení není platná.
* 406 – IoT Edge zařízení je offline nebo neodesílá zprávy o stavu.
* 500 – při IoT Edge modulu runtime došlo k chybě.

Další informace najdete v tématu [Agent IoT Edge](../articles/iot-edge/iot-edge-runtime.md?preserve-view=true&view=iotedge-2018-06#iot-edge-agent).

Následující chyba se týká služby IoT Edge na zařízení Azure Stack Edge pro.

### <a name="compute-modules-have-unknown-status-and-cant-be-used"></a>Výpočetní moduly mají neznámý stav a nejde je použít.

#### <a name="error-description"></a>Popis chyby

Všechny moduly v zařízení zobrazují neznámý stav a nelze je použít. Neznámý stav přetrvává při restartování.<!--Original Support ticket relates to trying to deploy a container app on a Hub. Based on the work item, I assume the error description should not be that specific, and that the error applies to Azure Stack Edge Devices, which is the focus of this troubleshooting.-->

#### <a name="suggested-solution"></a>Navrhované řešení

Odstraňte službu IoT Edge a znovu nasaďte moduly (y). Další informace najdete v tématu [Odebrání služby IoT Edge](../articles/databox-online/azure-stack-edge-j-series-manage-compute.md#remove-iot-edge-service).


### <a name="modules-show-as-running-but-are-not-working"></a>Moduly se zobrazují jako spuštěné, ale nefungují.

#### <a name="error-description"></a>Popis chyby

Běhový stav modulu se zobrazuje jako spuštěný, ale očekávaný výsledek se nezobrazuje. 

K tomuto stavu může dojít z důvodu problému s konfigurací směrování modulu, který nefunguje nebo `edgehub` nesměruje zprávy podle očekávání. Protokoly můžete kontrolovat `edgehub` . Pokud zjistíte, že došlo k chybám, jako je například selhání připojení ke službě IoT Hub, nejběžnějším důvodem jsou problémy s připojením. K problémům s připojením může dojít proto, že port AMPQ, který se používá jako výchozí port IoT Hub služby pro komunikaci, je blokovaný, nebo webový proxy server blokuje tyto zprávy.

#### <a name="suggested-solution"></a>Navrhované řešení

Postupujte následovně:
1. Tuto chybu můžete vyřešit tak, že přejdete na prostředek IoT Hub pro vaše zařízení a pak vyberete své hraniční zařízení. 
1. Přejít na **nastavit moduly > nastavení modulu runtime**. 
1. Přidejte `Upstream protocol` proměnnou prostředí a přiřaďte jí hodnotu `AMQPWS` . Zprávy nakonfigurované v tomto případě se odesílají přes objekty WebSockets přes port 443.

### <a name="modules-show-as-running-but-do-not-have-an-ip-assigned"></a>Moduly se zobrazují jako spuštěné, ale nemají přiřazenou IP adresu.

#### <a name="error-description"></a>Popis chyby

Běhový stav modulu se zobrazuje jako spuštěný, ale kontejnerová aplikace nemá přiřazenou IP adresu. 

Tato podmínka je způsobená tím, že rozsah IP adres, které jste zadali pro IP adresy externích služeb Kubernetes, není dostačující. Tento rozsah musíte zvětšit, abyste se ujistili, že jsou zahrnuté všechny kontejnery nebo virtuální počítače, které jste nasadili.

#### <a name="suggested-solution"></a>Navrhované řešení

V místním webovém uživatelském rozhraní zařízení proveďte následující kroky:
1. Přejít na stránku **COMPUTE** . Vyberte port, pro který jste povolili výpočetní síť. 
1. Zadejte statický a souvislý rozsah IP adres pro **IP adresy externích služeb Kubernetes**. Pro službu potřebujete 1 IP adresu `edgehub` . Kromě toho budete potřebovat jednu IP adresu pro každý IoT Edge modul a pro každý virtuální počítač, který nasadíte. 
1. Vyberte **Použít**. Změněný rozsah IP adres by měl platit okamžitě.

Další informace najdete v tématu [Změna IP adres externích služeb pro kontejnery](../articles/databox-online/azure-stack-edge-j-series-manage-compute.md#change-external-service-ips-for-containers).