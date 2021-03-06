---
title: zahrnout soubor
description: zahrnout soubor
services: functions
author: craigshoemaker
manager: gwallace
ms.service: azure-functions
ms.topic: include
ms.date: 08/02/2019
ms.author: cshoe
ms.custom: include file
ms.openlocfilehash: 938f55ae0ba911ea3a97cd49e6424bf8aaefdc76
ms.sourcegitcommit: d4734bc680ea221ea80fdea67859d6d32241aefc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2021
ms.locfileid: "100381680"
---
### <a name="default"></a>Výchozí

Pro vstupní vazbu objektu blob můžete použít následující typy parametrů:

* `Stream`
* `TextReader`
* `string`
* `Byte[]`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `ICloudBlob`<sup>první</sup>
* `CloudBlockBlob`<sup>první</sup>
* `CloudPageBlob`<sup>první</sup>
* `CloudAppendBlob`<sup>první</sup>

<sup>1</sup> vyžaduje vázání "InOut" `direction` v *function.js* v `FileAccess.ReadWrite` knihovně tříd jazyka C#.

Pokud se pokusíte vytvořit propojení s jedním z typů sad SDK úložiště a získat chybovou zprávu, ujistěte se, že máte odkaz na [správnou verzi sady SDK služby Storage](../articles/azure-functions/functions-bindings-storage-blob.md#azure-storage-sdk-version-in-functions-1x).

Vazba na `string` nebo `Byte[]` je doporučena pouze v případě, že velikost objektu BLOB je malá, protože celý obsah objektu BLOB je načten do paměti. Obecně je vhodnější použít `Stream` `CloudBlockBlob` typ nebo. Další informace naleznete v části [využití souběžnosti a paměti](../articles/azure-functions/functions-bindings-storage-blob-trigger.md#concurrency-and-memory-usage) výše v tomto článku.

### <a name="additional-types"></a>Další typy

Aplikace používající [5.0.0 nebo vyšší verze rozšíření úložiště](../articles/azure-functions/functions-bindings-storage-blob.md#storage-extension-5x-and-higher) můžou používat taky typy ze [sady Azure SDK pro .NET](/dotnet/api/overview/azure/storage.blobs-readme). Tato verze vyřazuje podporu pro starší `CloudBlobContainer` typy, `CloudBlobDirectory` ,,, `ICloudBlob` `CloudBlockBlob` `CloudPageBlob` a, a to `CloudAppendBlob` ve prospěch z následujících typů:

- [BlobContainerClient](/dotnet/api/azure.storage.blobs.blobcontainerclient)
- [BlobClient](/dotnet/api/azure.storage.blobs.blobclient)<sup>1</sup>
- [BlockBlobClient](/dotnet/api/azure.storage.blobs.specialized.blockblobclient)<sup>1</sup>
- [PageBlobClient](/dotnet/api/azure.storage.blobs.specialized.pageblobclient)<sup>1</sup>
- [AppendBlobClient](/dotnet/api/azure.storage.blobs.specialized.appendblobclient)<sup>1</sup>
- [BlobBaseClient](/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)<sup>1</sup>

<sup>1</sup> vyžaduje vázání "InOut" `direction` v *function.js* v `FileAccess.ReadWrite` knihovně tříd jazyka C#.

Příklady použití těchto typů najdete v [úložišti GitHub pro rozšíření](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/storage/Microsoft.Azure.WebJobs.Extensions.Storage.Blobs#examples).
