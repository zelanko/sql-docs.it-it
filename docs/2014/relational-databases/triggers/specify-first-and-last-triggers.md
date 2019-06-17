---
title: Specificare i primi e gli ultimi trigger | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- first triggers [SQL Server]
- last triggers
- DML triggers, first or last triggers
- INSTEAD OF triggers
- AFTER triggers
ms.assetid: 9e6c7684-3dd3-46bb-b7be-523b33fae4d5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a851a19a7f00afd055bb2ee8f00eaf4621a1e98f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62524137"
---
# <a name="specify-first-and-last-triggers"></a>Specifica dei primi e degli ultimi trigger
  È possibile specificare che uno dei trigger AFTER associati a una tabella sia il primo oppure l'ultimo trigger AFTER che viene attivato per ogni azione di trigger INSERT, DELETE e UPDATE. I trigger AFTER compresi fra il primo e l'ultimo vengono eseguiti in base a un ordine non definito.  
  
 Per specificare l'ordine per un trigger AFTER, usare la stored procedure **sp_settriggerorder** . **sp_settriggerorder** ha le opzioni seguenti.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**Primo**|Specifica che il trigger DML è il primo trigger AFTER attivato per un'azione di trigger.|  
|**Ultimo**|Specifica che il trigger DML è l'ultimo trigger AFTER attivato per un'azione di trigger.|  
|**None**|Specifica che non esiste un ordine specifico per l'attivazione del trigger DML. Viene utilizzata principalmente per reimpostare un trigger precedentemente designato come primo o ultimo.|  
  
 L'esempio seguente mostra l'utilizzo di **sp_settriggerorder**:  
  
```  
sp_settriggerorder @triggername = 'MyTrigger', @order = 'first', @stmttype = 'UPDATE'  
```  
  
> [!IMPORTANT]  
>  Il primo trigger e l'ultimo devono essere due trigger DML distinti.  
  
 Una tabella può includere contemporaneamente trigger INSERT, UPDATE e DELETE. È possibile impostare primo e ultimo trigger per ogni tipo di istruzione, ma non può trattarsi degli stessi trigger.  
  
 Se il primo o l'ultimo trigger definito per una tabella non copre un'azione di trigger, ad esempio non copre FOR UPDATE, FOR DELETE o FOR INSERT, per le azioni mancanti non esiste un primo o un ultimo trigger.  
  
 Non è possibile specificare i trigger INSTEAD OF come primi o ultimi trigger. I trigger INSTEAD OF vengono attivati prima dell'esecuzione degli aggiornamenti sulle tabelle sottostanti. Se un trigger INSTEAD OF esegue aggiornamenti sulle tabelle sottostanti, tali aggiornamenti vengono eseguiti prima dell'attivazione di qualsiasi trigger AFTER incluso nella tabella. Ad esempio, se un trigger INSTEAD OF INSERT su una vista inserisce dati in una tabella di base e tale tabella contiene un trigger INSTEAD OF INSERT e tre trigger AFTER INSERT, invece dell'azione di inserimento viene attivato il trigger INSTEAD OF INSERT della tabella di base e i trigger AFTER della tabella di base vengono attivati dopo l'esecuzione di qualsiasi azione di inserimento sulla tabella stessa. Per altre informazioni, vedere [DML Triggers](dml-triggers.md).  
  
 Se il primo o l'ultimo trigger viene modificato da un'istruzione ALTER TRIGGER, l'attributo **First** o **Last** viene rimosso e il valore relativo all'ordine viene impostato su **None**. È necessario reimpostare l'ordine usando **sp_settriggerorder**.  
  
 La funzione OBJECTPROPERTY usa le proprietà **ExecIsFirstTrigger** e **ExecIsLastTrigger**per segnalare se un trigger è primo o ultimo.  
  
 La replica genera automaticamente un primo trigger per ogni tabella inclusa in una sottoscrizione ad aggiornamento in coda o ad aggiornamento immediato. La replica richiede che il proprio trigger sia il primo trigger. La replica genera un errore se si cerca di includere una tabella con un primo trigger in una sottoscrizione ad aggiornamento immediato o ad aggiornamento in coda. Se si prova a impostare un trigger come primo dopo l'inclusione di una tabella in una sottoscrizione, **sp_settriggerorder** restituisce un errore. Se si usa ALTER sul trigger di replica oppure **sp_settriggerorder** per modificare il trigger di replica come ultimo trigger o come trigger senza un ordine di esecuzione specifico, la sottoscrizione non funzionerà in modo corretto.  
  
## <a name="see-also"></a>Vedere anche  
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectpropertyex-transact-sql)   
 [sp_settriggerorder &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql)  
  
  
