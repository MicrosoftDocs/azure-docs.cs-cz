---
title: Úhrada vyúčtování za Microsoft Azure
description: Zjistěte, jak uhradit vyúčtování na webu Azure Portal. Pokud chcete provádět platby na portálu, musíte být vlastníkem, přispěvatelem nebo správcem faktur daného fakturačního profilu.
keywords: billing, past due, balance, pay now,
author: banders
ms.reviewer: judupont
tags: billing, past due, pay now, bill, invoice, pay
ms.service: cost-management-billing
ms.subservice: billing
ms.topic: how-to
ms.date: 01/13/2021
ms.author: banders
ms.openlocfilehash: ecc5c8ebef0d2add365d128e11caedaa173d9d63
ms.sourcegitcommit: ec39209c5cbef28ade0badfffe59665631611199
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/12/2021
ms.locfileid: "103232139"
---
# <a name="how-to-pay-your-bill-for-microsoft-azure"></a>Postup placení vyúčtování služeb Microsoft Azure

Tento článek se týká zákazníků, kteří mají uzavřenou Smlouvu se zákazníkem Microsoftu (MCA).

[Kontrola přístupu ke smlouvě se zákazníkem Microsoftu](#check-access-to-a-microsoft-customer-agreement)

K dispozici jsou dva způsoby platby vyúčtování za Azure. Můžete platit buď prostřednictvím výchozího způsobu platby pro váš fakturační profil, nebo můžete provést jednorázovou platbu označenou jako **okamžitá úhrada**.

Pokud jste se do Azure zaregistrovali prostřednictvím zástupce společnosti Microsoft, je jako váš výchozí způsob platby vždycky nastavený *šek nebo bankovní převod*.

Pokud máte kredity Azure, automaticky se na fakturu uplatní každé fakturační období.

## <a name="pay-by-default-payment-method"></a>Platba pomocí výchozího způsobu platby

Výchozím způsobem platby pro váš fakturační profil může být kreditní nebo debetní karta, nebo šek či bezhotovostní převod.

### <a name="credit-or-debit-card"></a>Kreditní nebo debetní karta

Pokud výchozím způsobem platby pro váš fakturační profil je kreditní nebo debetní karta, každé fakturační období se automaticky strhne příslušná částka.

Pokud je automatická platba kreditní nebo debetní kartou z nějakého důvodu zamítnuta, můžete na webu Azure Portal provést jednorázovou platbu kreditní nebo debetní kartou pomocí **okamžité úhrady**.

Pokud chcete zjistit, jak změnit výchozí způsob platby na šek nebo bezhotovostní převod, přečtěte si téma [Jak platit pomocí faktury](../manage/pay-by-invoice.md).

### <a name="check-or-wire-transfer"></a>Šek nebo bezhotovostní převod

Pokud výchozím způsobem platby pro váš fakturační profil je šek nebo bezhotovostní převod, postupujte podle platebních pokynů uvedených v souboru PDF faktury.

Pokud výše faktury nedosahuje prahové hodnoty pro vaši měnu, můžete na webu Azure Portal provést jednorázovou platbu debetní nebo kreditní kartou pomocí možnosti **Zaplatit**. Pokud výše faktury překračuje tuto prahovou hodnotu, fakturu nejde uhradit kreditní nebo debetní kartou. Prahovou hodnotu pro vaši měnu najdete na webu Azure Portal po výběru **Zaplatit**.

## <a name="pay-now-in-the-azure-portal"></a>Platba na webu Azure Portal

Abyste mohli platit faktury na webu Azure Portal, musíte mít správná [oprávnění MCA](../manage/understand-mca-roles.md) nebo musíte být správcem fakturačního účtu. Správce fakturačního účtu je uživatel, který zaregistroval účet MCA.

1. Přihlaste se k webu [Azure Portal](https://portal.azure.com).
1. Vyhledejte **Cost Management a fakturace**.
1. V nabídce vlevo v části **Fakturace** vyberte **Faktury**.
1. Pokud jsou některé faktury splatné nebo po splatnosti, uvidíte u této faktury modrý odkaz **Zaplatit**. Vyberte **Zaplatit**.
1. V okně Zaplatit klikněte na **Vybrat způsob platby** a zvolte existující platební kartu, nebo přidejte novou.
1. Po výběru způsobu platby vyberte **Zaplatit**.

Stav faktury se během 24 hodin změní na *uhrazeno*.

## <a name="pay-now-for-customers-in-india"></a>Plaťte teď pro zákazníky v Indii.

Rezervovaná banka pro Indii vydala [Nová nařízení](https://www.rbi.org.in/Scripts/NotificationUser.aspx?Id=12002&Mode=0) , která vstoupí v platnost 1. dubna 2021. Po tomto datu mohou banky v Indii zahájit odmítnutí automatických opakovaných plateb a platby budou muset být provedeny ručně v Azure Portal.

Pokud vaše banka odmítne automatickou opakovanou platbu, pošleme vám e-mail s pokyny, jak pokračovat.

Od 1. dubna 2021 můžete uhradit zbývající zůstatek kdykoli pomocí následujících kroků: 

1. Přihlaste se na web [Azure Portal](https://portal.azure.com/) jako správce účtu.
1. Vyhledejte položku **Správa nákladů a fakturace**.
1. Na stránce Přehled vyberte tlačítko **platit nyní** . (Pokud nevidíte tlačítko **platit nyní** , nemáte zůstatek k dispozici.)

## <a name="check-access-to-a-microsoft-customer-agreement"></a>Kontrola přístupu k zákaznické smlouvě Microsoftu
[!INCLUDE [billing-check-mca](../../../includes/billing-check-mca.md)]

## <a name="next-steps"></a>Další kroky

- Pokud chcete mít nárok na platbu bankovním převodem nebo šekem, přečtěte si, [jak platit fakturou](../manage/pay-by-invoice.md).
