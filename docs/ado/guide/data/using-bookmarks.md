---
title: Uso dei segnalibri | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c7e14e063d1aabcfce6391a85c0fcddbf0ff4e9f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704612"
---
# <a name="using-bookmarks"></a>Uso dei segnalibri
È spesso utile restituire direttamente a un record specifico dopo aver visto spostamenti all'interno di **Recordset** senza dover scorrere tutti i record e confrontare i valori. Ad esempio, se si prova a cercare un record usando il **trovare** metodo, ma la ricerca non restituisce alcun record, viene automaticamente indirizzato alle due estremità della **Recordset**. Se il provider supporta questa funzionalità, i segnalibri possono essere usati per contrassegnare la stessa posizione prima di usare la **trovare** metodo in modo che è possibile tornare alla località. Un segnalibro è un **Variant** tipo di valore che identifica in modo univoco un record in un **Recordset** oggetto.  
  
 È anche possibile usare una matrice di varianti dei segnalibri con il **Recordset filtro** metodo per filtrare un set di record selezionato. Per informazioni dettagliate su questa tecnica, vedere filtrando i risultati nell'argomento [utilizzo di recordset](../../../ado/guide/data/working-with-recordsets.md), più avanti in questa sezione.  
  
 È possibile usare la **segnalibro** per ottenere un segnalibro per un record, o impostare il record corrente un **Recordset** oggetto nel record identificato da un segnalibro valido. Il codice seguente usa il **segnalibro** proprietà per impostare un segnalibro e quindi tornare al record di segnalibro dopo lo spostamento ai record di altri. Per determinare se le **Recordset** supporta segnalibri, utilizzare il **supporta** (metodo).  
  
```  
'BeginBookmarkEg  
Dim varBookmark As Variant  
Dim blnCanBkmrk As Boolean  
  
objRs.Open strSQL, strConnStr, adOpenStatic, adLockOptimistic, adCmdText  
  
If objRs.RecordCount > 4 Then  
    objRs.Move 4                       ' move to the fifth record  
    blnCanBkmrk = objRs.Supports(adBookmark)  
    If blnCanBkmrk = True Then  
        varBookmark = objRs.Bookmark   ' record the bookmark  
        objRs.MoveLast                 ' move to a different record  
        objRs.Bookmark = varBookmark   ' return to the bookmarked (sixth) record  
    End If  
End If  
'EndBookmarkEg  
```  
  
 Il [supporta](../../../ado/reference/ado-api/supports-method.md) metodo verrà discussa in modo più dettagliato più avanti.  
  
 Ad eccezione del caso di clonato **recordset**, i segnalibri sono univoci per il **Recordset** in cui sono stati creati, anche se viene usato lo stesso comando. Ciò significa che è possibile usare una **segnalibro** ottenute da uno **Recordset** spostare allo stesso record in un secondo **Recordset** aperta con lo stesso comando.
