---
title: Přehled překladu řeči – služba pro rozpoznávání řeči
titleSuffix: Azure Cognitive Services
description: Překlad řeči umožňuje přidat do aplikací, nástrojů a zařízení komplexní překlady řeči v reálném čase, který nabízí více jazyků. Stejné rozhraní API lze použít pro překlad řeči na řeč i řeči na text. Tento článek představuje přehled výhod a možností služby překladu řeči.
services: cognitive-services
author: erhopf
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 09/01/2020
ms.author: erhopf
ms.custom: devx-track-csharp, cog-serv-seo-aug-2020
keywords: Překlad řeči
ms.openlocfilehash: 36c2943d7cd5ce2c5c7c4a8501dc0033aa8c9cbc
ms.sourcegitcommit: 10d00006fec1f4b69289ce18fdd0452c3458eca5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/21/2020
ms.locfileid: "95015201"
---
# <a name="what-is-speech-translation"></a>Co je překlad řeči?

[!INCLUDE [TLS 1.2 enforcement](../../../includes/cognitive-services-tls-announcement.md)]

V tomto přehledu se dozvíte o výhodách a funkcích služby překladu řeči, která umožňuje překlad zvukových datových proudů v reálném čase na řeč a převod řeči na text. Pomocí sady Speech SDK mají vaše aplikace, nástroje a zařízení přístup ke zdroji přepisů a výstupům překladu pro daný zvuk. Průběžné výsledky přepisu a překladu se vrátí, protože se detekuje řeč a konečné výsledky je možné převést na syntetizované řeč.

Překladatelské modul společnosti Microsoft používá dva různé přístupy: statistická strojové překlady (SMT) a neuronové Machine Translation (NMT). SMT používá pokročilou statistickou analýzu k odhadu nejlepší možné překlady s ohledem na kontext několika slov. Pomocí NMT se sítě neuronové používají k zajištění přesnější a přirozeného akustického překladu pomocí úplného kontextu vět k překladu slov.

Dnes Microsoft používá NMT k překladu do nejoblíbenějších jazyků. Všechny [jazyky, které jsou k dispozici pro překlad řeči na řeč](language-support.md#speech-translation) , jsou napájeny pomocí NMT. Překlad řeči na text může v závislosti na páru jazyků používat SMT nebo NMT. Pokud je cílový jazyk podporován nástrojem NMT, úplný překlad je NMT. Pokud NMT cílový jazyk nepodporuje, je překlad hybridem NMT a SMT, a to pomocí angličtiny jako "Pivot" mezi dvěma jazyky.

## <a name="core-features"></a>Základní funkce

* Překlad řeči na text s výsledky rozpoznávání.
* Překlad řeči na řeč.
* Podpora překladu do více cílových jazyků.
* Výsledky dočasnáho rozpoznávání a překladu.

## <a name="get-started"></a>Začínáme 

Projděte si [rychlý Start](get-started-speech-translation.md) a začněte s překladem řeči. Služba překladu řeči je k dispozici prostřednictvím [sady Speech SDK](speech-sdk.md) a rozhraní příkazového [řádku pro rozpoznávání](spx-overview.md)řeči.

## <a name="sample-code"></a>Ukázka kódu

Vzorový kód pro sadu Speech SDK je k dispozici na GitHubu. Tyto ukázky se týkají běžných scénářů, jako je čtení zvuku ze souboru nebo datového proudu, nepřetržitého a jednorázového rozpoznávání/překladu a práce s vlastními modely.

* [Ukázky pro převod řeči na text a překlady (SDK)](https://github.com/Azure-Samples/cognitive-services-speech-sdk)

## <a name="migration-guides"></a>Průvodci migrací

Pokud vaše aplikace, nástroje nebo produkty používají [Translator Speech API](./how-to-migrate-from-translator-speech-api.md), vytvořili jsme příručky, které vám pomůžou s migrací na službu Speech.

* [Migrace z Translator Speech API do služby pro rozpoznávání řeči](how-to-migrate-from-translator-speech-api.md)

## <a name="reference-docs"></a>Referenční dokumenty

* [Speech SDK](./speech-sdk.md)
* [Speech Devices SDK](speech-devices-sdk.md)
* [REST API: Převod řeči na text](rest-speech-to-text.md)
* [REST API: převod textu na řeč](rest-text-to-speech.md)
* [REST API: přepis a přizpůsobení Batch](https://westus.dev.cognitive.microsoft.com/docs/services/speech-to-text-api-v3-0)

## <a name="next-steps"></a>Další kroky

* Dokončete [rychlý Start](get-started-speech-translation.md) překladu řeči.
* [Získejte zdarma klíč předplatného služby Speech](overview.md#try-the-speech-service-for-free)
* [Získat sadu Speech SDK](speech-sdk.md)