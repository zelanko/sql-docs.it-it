---
title: Specificare i primi e gli ultimi trigger | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1020bb9dff821471f33ba3af9285249a93980133
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68055995"
---
# <a name="specify-first-and-last-triggers"></a>Specifica dei primi e degli ultimi trigger
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  È possibile specificare che uno dei trigger AFTER associati a una tabella sia il primo oppure l'ultimo trigger AFTER che viene attivato per ogni azione di trigger INSERT, DELETE e UPDATE. I trigger AFTER compresi fra il primo e l'ultimo vengono eseguiti in base a un ordine non definito.  
  
 Per specificare l'ordine per un trigger AFTER, usare la stored procedure **sp_settriggerorder** . **sp_settriggerorder** ha le opzioni seguenti.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**Primo**|Specifica che il trigger DML è il primo trigger AFTER attivato per un'azione di trigger.|  
|**Ultimo**|Specifica che il trigger DML è l'ultimo trigger AFTER attivato per un'azione di trigger.|  
|**Nessuno**|Specifica che non esiste un ordine specifico per l'attivazione del trigger DML. Viene utilizzata principalmente per reimpostare un trigger precedentemente designato come primo o ultimo.|  
  
 L'esempio seguente mostra l'utilizzo di **sp_settriggerorder**:  
  
```  
sp_settriggerorder @triggername = 'MyTrigger', @order = 'first', @stmttype = 'UPDATE'  
```  
  
> [!IMPORTANT]  
>  Il primo trigger e l'ultimo devono essere due trigger DML distinti.  
  
 Una tabella può includere contemporaneamente trigger INSERT, UPDATE e DELETE. È possibile impostare primo e ultimo trigger per ogni tipo di istruzione, ma non può trattarsi degli stessi trigger.  
  
 Se il primo o l'ultimo trigger definito per una tabella non copre un'azione di trigger, ad esempio non copre FOR UPDATE, FOR DELETE o FOR INSERT, per le azioni mancanti non esiste un primo o un ultimo trigger.  
  
 Non è possibile specificare i trigger INSTEAD OF come primi o ultimi trigger. I trigger INSTEAD OF vengono attivati prima dell'esecuzione degli aggiornamenti sulle tabelle sottostanti. Se un trigger INSTEAD OF esegue aggiornamenti sulle tabelle sottostanti, tali aggiornamenti vengono eseguiti prima dell'attivazione di qualsiasi trigger AFTER incluso nella tabella. Ad esempio, se un trigger INSTEAD OF INSERT su una vista inserisce dati in una tabella di base e tale tabella contiene un trigger INSTEAD OF INSERT e tre trigger AFTER INSERT, invece dell'azione di inserimento viene attivato il trigger INSTEAD OF INSERT della tabella di base e i trigger AFTER della tabella di base vengono attivati dopo l'esecuzione di qualsiasi azione di inserimento sulla tabella stessa. Per altre informazioni, vedere [DML Triggers](../../relational-databases/triggers/dml-triggers.md).  
  
 Se il primo o l'ultimo trigger viene modificato da un'istruzione ALTER TRIGGER, l'attributo **First** o **Last** viene rimosso e il valore relativo all'ordine viene impostato su **None**. È necessario reimpostare l'ordine usando **sp_settriggerorder**.  
  
 La funzione OBJECTPROPERTY indica se un trigger è un primo o ultimo trigger tramite le proprietà seguenti: **ExecIsFirstInsertTrigger**, **ExecIsFirstUpdateTrigger**, **ExecIsFirstDeleteTrigger**, **ExecIsLastInsertTrigger**, **ExecIsLastUpdateTrigger** e **ExecIsLastDeleteTrigger**.  
  
 La replica genera automaticamente un primo trigger per ogni tabella inclusa in una sottoscrizione ad aggiornamento in coda o ad aggiornamento immediato. La replica richiede che il proprio trigger sia il primo trigger. La replica genera un errore se si cerca di includere una tabella con un primo trigger in una sottoscrizione ad aggiornamento immediato o ad aggiornamento in coda. Se si prova a impostare un trigger come primo dopo l'inclusione di una tabella in una sottoscrizione, **sp_settriggerorder** restituisce un errore. Se si usa ALTER sul trigger di replica oppure **sp_settriggerorder** per modificare il trigger di replica come ultimo trigger o come trigger senza un ordine di esecuzione specifico, la sottoscrizione non funzionerà in modo corretto.  
  
## <a name="see-also"></a>Vedere anche  
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_settriggerorder &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md)  
  
  
