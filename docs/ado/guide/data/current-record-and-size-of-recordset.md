---
title: Record corrente e le dimensioni del Recordset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a01e17ea9c786a724e5869a28bf4d8927b58ac81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925699"
---
# <a name="current-record-and-size-of-recordset"></a>Record corrente e dimensioni del recordset
In questa sezione viene descritto come individuare la posizione corrente del cursore nel campione **Recordset** nelle [esempio di codice JScript per restituire un Recordset](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md).  
  
## <a name="current-record"></a>Record corrente  
 Il record corrente nel set di dati corrisponde a che la posizione del cursore di cui punta il **Recordset** oggetto. Quando un **Recordset** oggetto viene restituito dall'origine dati come risultato della chiamata al metodo **Open**, **Command. Execute**, o **Connection. Execute**  (tra cui **Connection.NamedCommand** e **Connection.StoredProcedure**), il cursore viene impostato in modo da puntare al primo record. Il set di dati di esempio, il record corrente iniziale è "Frutta polvere organica pere" elemento.  
  
## <a name="size-of-recordset"></a>Dimensioni del Recordset  
 Per trovare la dimensione di un **Recordset** dell'oggetto, ottenere il valore della **Recordset.RecordCount** proprietà. Questo valore è un valore long integer che indica il numero di record nel **Recordset**. Se il set di dati viene restituito dal Provider OLE DB per Microsoft SQL Server, questo valore indica il numero di righe restituite. Leggere il **RecordCount** proprietà in una classe chiusa **Recordset** provoca un errore.  
  
 Se non è possibile determinare il numero di record, il valore della proprietà è -1.  
  
 Il valore della **RecordCount** proprietà dipende anche dalle funzionalità del provider e il tipo di cursore utilizzato. Per un cursore forward-only, il valore è -1. Per un cursore keyset o statico, il valore è il numero effettivo di record restituiti nel **Recordset** oggetto. Per un cursore dinamico, il valore è -1 o il numero effettivo di record, a seconda dell'origine dati.  
  
 Un cursore che supporta **Recordcount** necessario lavoro più difficili e pertanto richiede più potenza di calcolo, rispetto a un cursore non supporta **Recordcount**. Se non occorre conoscere il numero di record, usando il tipo di cursore diverso potrebbe contribuire a migliorare le prestazioni dell'applicazione, soprattutto se devono gestire grandi set di dati.  
  
 In alcuni casi, un cursore o il provider non riesce a determinare il **RecordCount** valore senza prima recuperare tutti i record dall'origine dati. Per garantire l'accuratezza del conteggio, chiamare il **Recordset**. **MoveLast** metodo prima di chiamare **Recordset.RecordCount**.  
  
 L'esempio **Recordset** ottenuto usando l'oggetto il [esempio di codice JScript](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md) Usa un cursore forward-only, quindi la chiamata **RecordCount** tohoto objektu comporta sempre -1. Se si modifica la riga di codice che chiama il **Recordset**. **Aprire** metodo come illustrato nell'esempio seguente, il **RecordCount** proprietà restituirà il numero effettivo di record recuperati.  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 Infatti, statico cursori con il [Provider Microsoft OLE DB per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) supportano **RecordCount**. In questo esempio sono presenti cinque record e di conseguenza **RecordCount** deve restituire il valore 5.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
 [Limiti di un recordset](../../../ado/guide/data/boundaries-of-a-recordset.md)
