---
title: Altre modalità di spostamento in un Recordset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ea83f40c6d6e595277a173c181c24f33e382393
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924883"
---
# <a name="more-ways-to-move-in-a-recordset"></a>Altri metodi per lo spostamento in un recordset
I quattro metodi seguenti consentono di spostarsi all'interno o di scorrimento, nelle **Recordset**: [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md). (Alcuni di questi metodi sono disponibili sui cursori forward-only).  
  
 **Metodi MoveFirst** diventa la posizione corrente del primo record la **Recordset**. **MoveLast** modifica il record corrente all'ultima posizione il record nel **Recordset**. Per utilizzare **MoveFirst** oppure **MoveLast**, il **Recordset** oggetto deve supportare lo spostamento del cursore con le versioni precedenti o i segnalibri; in caso contrario, la chiamata al metodo genererà un errore.  
  
 **MoveNext** sposta il record corrente posizionare un'unica posizione in avanti. Se si usa l'ultimo record durante la chiamata **MoveNext**, **EOF** verrà impostato su **True**. **MovePrevious** sposta il record corrente posizionare un'unica posizione con le versioni precedenti. Se si usa il primo record quando si chiama **MovePrevious**, **BOF** verrà impostato su **True**. È consigliabile verificare i **EOF** e **BOF** delle proprietà quando si usano questi metodi e per spostare il cursore in un posizione valida del record corrente se si sposta da delle estremità del **Recordset**, come illustrato di seguito:  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 O, nel caso del **MovePrevious** metodo:  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 Nei casi in cui il **Recordset** è stato filtrato o ordinato e i dati del record corrente viene modificati, può anche cambiare la posizione. In questi casi il **MoveNext** metodo funziona normalmente, ma tenere presente che la posizione viene spostato un record in avanti dalla nuova posizione, non rispetto alla posizione precedente. Ad esempio, modificando i dati del record corrente, in modo che il record viene spostato alla fine della ordinato **Recordset**, significa che la chiamata **MoveNext** comporta l'impostazione del record corrente il posizione successiva all'ultimo record nel **Recordset** (**EOF** = **True**).  
  
 Il comportamento delle diverse modalità di spostamento i **Recordset** oggetto dipende, in una certa misura, sui dati all'interno di **Recordset**. Nuovi record aggiunti per il **Recordset** vengono inizialmente aggiunte in un determinato ordine, che dipende dall'origine dati e può essere dipendenti in modo implicito o esplicito sui dati nel nuovo record. Ad esempio, se un ordinamento o un join viene eseguito all'interno della query che popola la **Recordset**, verrà inserito il nuovo record nella posizione appropriata all'interno di **Recordset**. Se l'ordinamento non viene specificato esplicitamente durante la creazione di **Recordset**, le modifiche nell'implementazione dell'origine dati possono comportare l'ordinamento delle righe restituite modificare inavvertitamente. In aggiunta, l'ordinamento, filtro e modifica delle funzioni dei **Recordset** possono influire sull'ordine e probabilmente saranno visibili le righe nel recordset.  
  
 Pertanto **MoveNext**, **MovePrevious**, **MoveFirst**, **MoveLast**, e **spostare** sono tutti distinzione ad altre operazioni eseguite sulla stessa **Recordset**. ADO tenterà sempre di mantenere la posizione corrente fino a quando non spostare in modo esplicito, ma in alcuni casi, le nuove modifiche rendono difficile da comprendere gli effetti di un'operazione di spostamento successiva. Ad esempio, se si chiama **MoveFirst** alla posizione della prima riga di un controllo ordinato **Recordset** e si modifica l'ordinamento da crescente a decrescente, che trovano ancora nella stessa riga - ma ora è l'ultima riga nel **Recordset**. **Metodi MoveFirst** verrà visualizzata una riga diversa (nuova prima riga).  
  
 Un altro esempio, se si è posizionati in una determinata riga al centro di un **Recordset** e si chiama **eliminare** e quindi chiamare **MoveNext**, è ora disponibile su record subito dopo il record eliminato. Ma la chiamata **MovePrevious** il record precedente quello eliminato il record corrente, poiché il record eliminato non viene più considerato nell'abbonamento attivo delle **Recordset**.  
  
 È particolarmente difficile da definire la semantica di spostamento coerente in tutti i provider per i metodi che gestiscono lo spostamento relativo al record corrente - **MovePrevious**, **MoveNext**, e **spostare** : in caso di modifica dei dati presenti nel record corrente. Ad esempio, se si lavora con un ordinati, filtrati **Recordset**e si modificano i dati presenti nel record corrente in modo che precedano tutti gli altri record, ma i dati modificati anche non corrispondano più al filtro, non è chiaro dove un **MoveNext** operazione dovrebbe venire visualizzata. La conclusione più sicura è lo spostamento relativo all'interno di un **Recordset** è più rischioso di movimento assoluto (ad esempio l'uso **MoveFirst** oppure **MoveLast**) quando i dati sono la modifica durante la modifica, i record aggiunti o eliminati. Ordinamento e filtro deve essere basate su una chiave primaria o un ID, poiché questo tipo di valore non deve cambiare.
