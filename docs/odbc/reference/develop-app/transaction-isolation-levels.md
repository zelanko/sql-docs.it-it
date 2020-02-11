---
title: Livelli di isolamento delle transazioni (ODBC) | Microsoft Docs
ms.custom: seo-dt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- dirty reads [ODBC]
- isolation levels [ODBC]
- nonrepeatable reads [ODBC]
- read uncommitted [ODBC]
- read committed [ODBC]
- serializable reads [ODBC]
- phantoms [ODBC]
- transaction isolation [ODBC]
- repeatable reads [ODBC]
- transactions [ODBC], isolation
ms.assetid: 0d638d55-ffd0-48fb-834b-406f466214d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e11a0d76fc4a2daece7b6f4f50761d40933792be
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73637214"
---
# <a name="transaction-isolation-levels-odbc"></a>Livelli di isolamento delle transazioni (ODBC)
I *livelli di isolamento delle transazioni* sono una misura dell'ambito di esito positivo dell'isolamento delle transazioni. In particolare, i livelli di isolamento delle transazioni sono definiti dalla presenza o dall'assenza dei seguenti fenomeni:  
  
-   **Letture dirty** Una *lettura dirty* si verifica quando una transazione legge i dati di cui non è ancora stato eseguito il commit. Si supponga, ad esempio, che Transaction 1 aggiorni una riga. La transazione 2 legge la riga aggiornata prima del commit dell'aggiornamento da parte della transazione 1. Se la transazione 1 esegue il rollback della modifica, la transazione 2 disporrà di dati di lettura considerati mai esistenti.  
  
-   **Letture non ripetibili** Una *lettura non ripetibile* si verifica quando una transazione legge la stessa riga due volte, ma restituisce ogni volta dati diversi. Si supponga, ad esempio, che la transazione 1 legga una riga. La transazione 2 aggiorna o Elimina la riga ed Esegui il commit dell'aggiornamento o dell'eliminazione. Se la transazione 1 rilegge la riga, recupera valori di riga diversi o rileva che la riga è stata eliminata.  
  
-   **Righe fantasma** Un oggetto *Phantom* è una riga che corrisponde ai criteri di ricerca, ma non viene inizialmente visualizzata. Si supponga, ad esempio, che Transaction 1 legga un set di righe che soddisfano i criteri di ricerca. La transazione 2 genera una nuova riga (tramite un aggiornamento o un inserimento) che corrisponde ai criteri di ricerca per la transazione 1. Se Transaction 1 esegue nuovamente l'istruzione che legge le righe, ottiene un set di righe diverso.  
  
 I quattro livelli di isolamento delle transazioni (definiti da SQL-92) sono definiti in termini di questi fenomeni. Nella tabella seguente, una "X" contrassegna ogni fenomeno che può verificarsi.  
  
|Livello di isolamento delle transazioni|Letture dirty|Letture non ripetibili|Fantasmi|  
|---------------------------------|-----------------|-------------------------|--------------|  
|Read Uncommitted|X|X|X|  
|Read Committed|--|X|X|  
|Repeatable Read|--|--|X|  
|Serializable|--|--|--|  
  
 Nella tabella seguente vengono descritte le modalità semplici con cui un sistema DBMS può implementare i livelli di isolamento delle transazioni.  
  
> [!IMPORTANT]  
>  La maggior parte dei DBMS usa schemi più complessi di quelli per aumentare la concorrenza. Questi esempi vengono forniti solo a scopo illustrativo. In particolare, ODBC non prescrive il modo in cui determinati DBMS isolano le transazioni l'una dall'altra.  
  
|Isolamento delle transazioni|Implementazione possibile|  
|---------------------------|-----------------------------|  
|Read Uncommitted|Le transazioni non sono isolate l'una dall'altra. Se il sistema DBMS supporta altri livelli di isolamento delle transazioni, ignorerà qualsiasi meccanismo utilizzato per implementare tali livelli. In modo che non influiscano negativamente sulle altre transazioni, le transazioni in esecuzione al livello Read uncommitted sono in genere di sola lettura.|  
|Read Committed|La transazione resta in attesa fino a quando non vengono sbloccate le righe con blocco Write da altre transazioni. in questo modo si impedisce la lettura di dati "Dirty".<br /><br /> La transazione include un blocco di lettura (se legge solo la riga) o un blocco di scrittura (se la riga viene aggiornata o eliminata) nella riga corrente per impedire ad altre transazioni di aggiornarla o eliminarla. La transazione rilascia i blocchi di lettura quando si sposta dalla riga corrente. Include i blocchi di scrittura finché non viene eseguito il commit o il rollback.|  
|Repeatable Read|La transazione resta in attesa fino a quando non vengono sbloccate le righe con blocco Write da altre transazioni. in questo modo si impedisce la lettura di dati "Dirty".<br /><br /> La transazione include i blocchi di lettura in tutte le righe restituite all'applicazione e scrive i blocchi in tutte le righe inserite, aggiornate o eliminate. Se, ad esempio, la transazione include l'istruzione **SQL \* Select from Orders, tramite**la transazione Read-Locks vengono bloccate le righe durante le quali vengono recuperate dall'applicazione. Se la transazione include l'istruzione SQL **Delete da Orders in cui status =' Closed '**, la transazione scrive i blocchi delle righe durante l'eliminazione.<br /><br /> Poiché le altre transazioni non possono aggiornare o eliminare queste righe, la transazione corrente evita le letture non ripetibili. La transazione rilascia i blocchi quando ne viene eseguito il commit o il rollback.|  
|Serializable|La transazione resta in attesa fino a quando non vengono sbloccate le righe con blocco Write da altre transazioni. in questo modo si impedisce la lettura di dati "Dirty".<br /><br /> La transazione include un blocco di lettura (se legge solo le righe) o il blocco di scrittura (se può aggiornare o eliminare righe) nell'intervallo di righe a cui ha effetto. Se, ad esempio, la transazione include l'istruzione **SQL \* Select from Orders**, l'intervallo sarà costituito dall'intera tabella Orders. la transazione Read-blocca la tabella e non consente l'inserimento di nuove righe. Se la transazione include l'istruzione SQL **Delete da Orders in cui status =' Closed '**, l'intervallo è costituito da tutte le righe con lo stato "closed"; la transazione Write-blocca tutte le righe della tabella Orders con lo stato "CLOSED" e non consente l'inserimento o l'aggiornamento di righe in modo che la riga risultante abbia lo stato "CLOSED".<br /><br /> Poiché le altre transazioni non possono aggiornare o eliminare le righe nell'intervallo, la transazione corrente evita le letture non ripetibili. Poiché le altre transazioni non possono inserire righe nell'intervallo, la transazione corrente evita eventuali oggetti fantasma. La transazione rilascia il blocco quando ne viene eseguito il commit o il rollback.|  
  
 È importante notare che il livello di isolamento della transazione non influisce sulla capacità di una transazione di visualizzare le proprie modifiche; le transazioni possono sempre visualizzare tutte le modifiche apportate. Una transazione, ad esempio, può essere costituita da due istruzioni **Update** , la prima delle quali genera il pagamento di tutti i dipendenti del 10% e la seconda imposta il pagamento di tutti i dipendenti su una quantità massima. Questa operazione ha esito positivo solo perché la seconda istruzione **Update** può visualizzare i risultati della prima.
