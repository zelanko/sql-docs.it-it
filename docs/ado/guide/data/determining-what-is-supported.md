---
title: Determinazione delle funzionalità supportate | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c6af51d8d69f5897021733468ee93290e1b5e280
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702089"
---
# <a name="determining-what-is-supported"></a>Determinazione delle funzionalità supportate
Il **supporta** metodo viene utilizzato per determinare se un determinato **Recordset** oggetto supporta un determinato tipo di funzionalità. Presenta la sintassi seguente:  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>Note  
 Il **supporta** metodo restituisce un valore booleano che indica se il provider supporta tutte le funzionalità identificate dall'argomento CursorOptions. È possibile usare la **supporta** metodo per determinare quali tipi di funzionalità di un **Recordset** supporta dell'oggetto. Se il **Recordset** oggetto supporta le funzionalità di cui costanti corrispondente sono *CursorOptions*, il **supporta** restituzione del metodo **True**. In caso contrario, restituisce **False**.  
  
 Usando il **supporta** metodo, è possibile cercare la capacità del **Recordset** oggetto per aggiungere nuovi record, usare i segnalibri, usare il **trovare** metodo, utilizzare lo scorrimento, utilizzare il  **Indice** proprietà, nonché per eseguire gli aggiornamenti in batch. Per un elenco completo di costanti e i relativi significati, vedere [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md).  
  
 Anche se il **supporta** metodo può restituire **True** per una determinata funzionalità, ma questa soluzione non garantisce che il provider può rendere la funzionalità disponibile in tutte le circostanze. Il **supporta** metodo restituisce semplicemente se il provider supporta la funzionalità specificata, presupponendo che vengano soddisfatte determinate condizioni. Ad esempio, il **supporta** metodo potrebbe indicare che un **Recordset** oggetto supporti gli aggiornamenti, anche se il cursore è basato su un join tra più tabelle - alcune colonne di cui non sono aggiornabili.
