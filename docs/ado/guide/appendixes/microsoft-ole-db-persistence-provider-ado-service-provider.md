---
title: Provider di persistenza Microsoft OLE DB (ADO Service Provider) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2bd341a3af2d1fdb076312b4c0993184fb4fae39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926762"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Panoramica di Provider Microsoft OLE DB Persistence
Provider Microsoft OLE DB Persistence consente di salvare un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) dell'oggetto in un file e il ripristino in un secondo momento che **Recordset** oggetto dal file. Le informazioni sullo schema, i dati e le modifiche in sospeso vengono mantenute.

 È possibile salvare il **Recordset** in formato avanzata dei dati nella tabella gramma (ADTG) proprietarie o open formato Extensible Markup Language (XML).

## <a name="provider-keyword"></a>Parola chiave provider
 Per richiamare questo provider, specificare la parola chiave e il valore seguenti nella stringa di connessione.

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>Errors
 I seguenti errori generati da questo provider possono essere rilevati nell'applicazione.

|Costante|Descrizione|
|--------------|-----------------|
|E_BADSTREAM|File aperto non dispone di un formato valido (vale a dire, il formato non è ADTG o XML).|
|E_CANTPERSISTROWSET|Il **Recordset** salvato l'oggetto presenta caratteristiche che ne impediscono l'archiviazione.|

## <a name="remarks"></a>Note
 Provider Microsoft OLE DB Persistence non espone proprietà dinamiche.

 Attualmente, solo con parametri gerarchici **Recordset** oggetti non possono essere salvati.

 Per altre informazioni sulla memorizzazione persistente **Recordset** oggetti, vedere [persistenza dei Recordset](../../../ado/guide/data/more-about-recordset-persistence.md).

 Quando si usa un flusso per aprire una **Recordset,** non deve essere presente nessun parametro specificato diverso il *origine* parametro del **aprire** (metodo).

## <a name="see-also"></a>Vedere anche
[Provider di persistenza Microsoft OLE DB (ADO Service Provider)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
