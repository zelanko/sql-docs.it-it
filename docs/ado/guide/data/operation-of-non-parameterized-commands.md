---
title: Funzionamento dei comandi senza parametri | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- non-parameterized commands [ADO]
- data shaping [ADO], non-parameterized commands
ms.assetid: 9700e50a-9f17-4ba3-8afb-f750741dc6ca
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 40677971cc2bc5b97c62aad1e638e52deb24c67e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700533"
---
# <a name="operation-of-non-parameterized-commands"></a>Funzionamento dei comandi senza parametri
Per i comandi senza parametri, vengono eseguiti tutti i comandi di provider e il **recordset** vengono creati durante l'esecuzione del comando. Se il comando viene eseguito in modo sincrono, tutti i **recordset** verrà popolato completamente. Se è stata selezionata una modalità di popolamento asincrono, lo stato di popolamento del **recordset** variano in base alla modalità di popolamento e la dimensione delle **recordset**.  
  
 Ad esempio, il *comando padre* potrebbe restituire una **Recordset** dei clienti per una società da una tabella Customers e il *comando figlio* potrebbe restituire un **Recordset** degli ordini per tutti i clienti da una tabella degli ordini.  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 Per le relazioni padre-figlio senza parametri, ogni elemento padre e figlio **Recordset** oggetto deve avere una colonna in comune per associarli. Le colonne sono denominate nella clausola RELATE *colonna padre* prima e quindi *colonna figlio*. Le colonne possono avere nomi diversi nei rispettivi **Recordset** oggetti, ma deve fare riferimento alle stesse informazioni per specificare una relazione significativa. Ad esempio, il **clienti** e **ordini Recordset** oggetti potrebbe avere un campo customerID. Poiché l'appartenenza dell'elemento figlio **Recordset** è determinato dal comando del provider, l'elemento figlio **Recordset** possono contenere righe orfane. Queste righe orfane non sono accessibili senza modificare la forma aggiuntive.  
  
 Il data shaping aggiunge una colonna a capitoli all'elemento padre **Recordset**. I valori nella colonna del capitolo sono i riferimenti alle righe nell'elemento figlio **Recordset**, che soddisfano la clausola RELATE. Lo stesso valore è nel *colonna padre* di una riga padre specificato come è la *colonna figlio* di tutte le righe dell'oggetto figlio capitolo. Quando più clausole TO vengono utilizzate nella clausola RELATE stesso, vengono combinati in modo implicito usando l'operatore AND. Se le colonne nella clausola RELATE padre non costituiscono una chiave per l'elemento padre **Recordset**, una riga di singolo elemento figlio può avere più righe padre.  
  
 Quando si accede al riferimento nella colonna del capitolo, ADO recupererà automaticamente il **Recordset** rappresentata dal riferimento. Si noti che in un comando senza parametri, anche se l'elemento figlio intera **Recordset** è stato recuperato, il capitolo include solo un subset di righe.  
  
 Se non include la colonna accodata *capitolo-alias*, verrà generato un nome per tale automaticamente. Oggetto [campo](../../../ado/reference/ado-api/field-object.md) la colonna verrà aggiunta al relativo oggetto il **Recordset** dell'oggetto [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta e il relativo tipo di dati sarà **adChapter**.  
  
 Per informazioni sulla navigazione gerarchico **Recordset**, vedere [accesso alle righe in un Recordset gerarchico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Grammatica formale per Shape](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandi Shape in generale](../../../ado/guide/data/shape-commands-in-general.md)
