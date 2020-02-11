---
title: Uso di segnalibri | Microsoft Docs
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
ms.openlocfilehash: 9fa2a738a3e94cd306619a318b75a2fd506972c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923614"
---
# <a name="using-bookmarks"></a>Uso dei segnalibri
Spesso è utile tornare direttamente a un record specifico dopo aver spostato il **Recordset** senza dover scorrere ogni record e confrontare i valori. Se, ad esempio, si tenta di cercare un record utilizzando il metodo **Find** , ma la ricerca non restituisce alcun record, si viene posizionati automaticamente a una delle estremità del **Recordset**. Se il provider li supporta, è possibile usare i segnalibri per contrassegnare il posto prima di usare il metodo **Find** , in modo da poter tornare al percorso. Un segnalibro è un valore di tipo **Variant** che identifica in modo univoco un record in un oggetto **Recordset** .  
  
 È anche possibile usare una matrice Variant di segnalibri con il metodo di **filtro Recordset** per filtrare in un set di record selezionato. Per informazioni dettagliate su questa tecnica, vedere filtro dei risultati nell'argomento [utilizzo di recordset](../../../ado/guide/data/working-with-recordsets.md), più avanti in questa sezione.  
  
 È possibile utilizzare la proprietà **Bookmark** per ottenere un segnalibro per un record o impostare il record corrente in un oggetto **Recordset** sul record identificato da un segnalibro valido. Il codice seguente usa la proprietà **Bookmark** per impostare un segnalibro e quindi tornare al record con segnalibro dopo aver spostato gli altri record. Per determinare se il **Recordset** supporta segnalibri, utilizzare il metodo **Supports** .  
  
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
  
 Il metodo [Supports](../../../ado/reference/ado-api/supports-method.md) viene trattato in modo più dettagliato in un secondo momento.  
  
 Ad eccezione del caso di **Recordset**clonati, i segnalibri sono univoci per il **Recordset** in cui sono stati creati, anche se viene usato lo stesso comando. Ciò significa che non è possibile utilizzare un **segnalibro** ottenuto da un **Recordset** per spostarsi nello stesso record in un secondo **Recordset** aperto con lo stesso comando.
