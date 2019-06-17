---
title: Uso delle pagine | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- PageSize property [ADO]
- pages [ADO]
- Recordset object [ADO]
- AbsolutePage property [ADO]
- PageCount property [ADO]
ms.assetid: 442b08c5-ccc7-4192-a1cc-22f250867782
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6afd68ddf99799288939eeb0c6522275ec4d273f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704532"
---
# <a name="using-pages"></a>Uso delle pagine
Usare la **PageCount** proprietà per determinare il numero di pagine di dati presenti nel **Recordset** oggetto. *Le pagine* sono gruppi di record con dimensioni uguali i **PageSize** l'impostazione della proprietà. Anche se l'ultima pagina incompleta perché sono presenti record minore del **PageSize** valore, viene conteggiata come una pagina aggiuntiva nel **PageCount** valore. Se il **Recordset** oggetto non supporta questa proprietà, **PageCount** sarà -1 per indicare che il **PageCount** non è possibile determinare.  
  
 Usare la **PageSize** proprietà per determinare il numero di record che costituiscono una pagina logica dei dati. La definizione di una dimensione di pagina consente di usare la **AbsolutePage** proprietà per passare al primo record di una pagina particolare. Ciò è utile negli scenari di server Web quando si vuole consentire all'utente di pagine di dati, visualizzazione di un determinato numero di record alla volta.  
  
 Questa proprietà può essere impostata in qualsiasi momento e il relativo valore verrà utilizzato per calcolare la posizione del primo record di una pagina particolare.  
  
 Usare la **AbsolutePage** proprietà per identificare il numero di pagina in cui si trova il record corrente. Anche in questo caso, il provider deve supportare le funzionalità appropriate per questa proprietà sia disponibile.  
  
 **Proprietà AbsolutePage** è basato su 1 e uguale a 1 quando il record corrente è il primo record nel **Recordset**. Impostare questa proprietà per spostare il primo record di una pagina particolare. Ottenere il numero totale di pagine dal **PageCount** proprietà.
