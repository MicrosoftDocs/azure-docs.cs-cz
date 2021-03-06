---
title: Přehled portfolia agenta a podpora operačního systému
description: Azure Defender pro IoT poskytuje velké portfolio agentů na základě typu zařízení.
author: shhazam-ms
manager: rkarlin
ms.author: shhazam
ms.date: 1/20/2021
ms.topic: quickstart
ms.service: azure
ms.openlocfilehash: e2897018d1695bde665e1d1aca180e5268851a0b
ms.sourcegitcommit: dac05f662ac353c1c7c5294399fca2a99b4f89c8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/04/2021
ms.locfileid: "102120143"
---
# <a name="agent-portfolio-overview-and-os-support"></a>Přehled portfolia agenta a podpora operačního systému 

Azure Defender pro IoT poskytuje velké portfolio agentů na základě typu zařízení. 

## <a name="standalone-agent"></a>Samostatný Agent

Samostatný agent pokrývá většinu operačních systémů Linux, které je možné nasadit jako binární balíček, nebo jako zdrojový kód, který je možné začlenit jako součást firmwaru, a umožňuje úpravy a přizpůsobení na základě zákaznických potřeb. Příklad podpory operačního systému: 

| Operační systém | AMD | ARM32v7 |
|--|--|--|
| Debian 9 | ✓ | ✓ |
| Ubuntu 18.04 | ✓ |  |
| Ubuntu 20.04 | ✓ |  |

Pokud chcete získat další informace, podporu operačního systému nebo požádat o přístup ke zdrojovému kódu, abyste ho mohli začlenit jako součást firmwaru zařízení, kontaktujte svého správce účtů nebo pošlete e-mail na adresu <defender_micro_agent@microsoft.com> . 

## <a name="azure-rtos-micro-agent"></a>Agent Azure RTO Micro

Agent Azure Defender pro IoT Micro poskytuje komplexní a zjednodušené řešení zabezpečení pro zařízení, která používají Azure RTO. Azure Defender pro IoT Micro agent poskytuje pokrytí pro běžné hrozby a potenciální škodlivé aktivity na zařízeních s operačním systémem v reálném čase (RTO). Mikroagenti jsou vestavěná v rámci součásti Azure RTO NetX Duo a monitorují aktivitu sítě v zařízení. 

Agent Azure Defender pro IoT Micro je integrovaný jako součást součásti Azure RTO NetX Duo a sleduje činnost v síti zařízení. Mikroagent se skládá z komplexního a zjednodušeného řešení zabezpečení, které poskytuje pokrytí pro běžné hrozby a potenciální škodlivé aktivity na zařízeních s operačním systémem v reálném čase (RTO).

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o nástroji [Standalone Micro agent ](concept-standalone-micro-agent-overview.md).