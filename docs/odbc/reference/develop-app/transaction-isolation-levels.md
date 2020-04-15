---
title: Livelli di isolamento delle transazioni (ODBC, Transaction Isolation Levels) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 622b4cd7f0db259b5ecfd5be63b27df64be965e7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298034"
---
# <a name="transaction-isolation-levels-odbc"></a>Livelli di isolamento delle transazioni (ODBC)Transaction Isolation Levels (ODBC)
I livelli di isolamento delle *transazioni* sono una misura della misura in cui l'isolamento delle transazioni ha esito positivo. In particolare, i livelli di isolamento delle transazioni sono definiti dalla presenza o dall'assenza dei seguenti fenomeni:  
  
-   **Letture sporche** Una *lettura dirty* si verifica quando una transazione legge i dati di cui non è ancora stato eseguito il commit. Si supponga, ad esempio, che la transazione 1 aggiorni una riga. La transazione 2 legge la riga aggiornata prima che la transazione 1 esetrai il commit dell'aggiornamento. Se la transazione 1 esegue il rollback della modifica, la transazione 2 dirà dati letti che si ritiene non siano mai esistiti.  
  
-   **Letture non ripetibili** Una *lettura non ripetibile* si verifica quando una transazione legge la stessa riga due volte, ma ottiene dati diversi ogni volta. Si supponga, ad esempio, che la transazione 1 legga una riga. La transazione 2 aggiorna o elimina tale riga ed esegue il commit dell'aggiornamento o dell'eliminazione. Se la transazione 1 rilegge la riga, recupera valori di riga diversi o rileva che la riga è stata eliminata.  
  
-   **Fantasmi** Un *fantasma* è una riga che corrisponde ai criteri di ricerca ma non viene visualizzata inizialmente. Si supponga, ad esempio, che la transazione 1 legga un set di righe che soddisfano alcuni criteri di ricerca. La transazione 2 genera una nuova riga (tramite un aggiornamento o un inserimento) che corrisponde ai criteri di ricerca per la transazione 1. Se la transazione 1 esegue nuovamente l'istruzione che legge le righe, ottiene un set di righe diverso.  
  
 I quattro livelli di isolamento delle transazioni (come definito da SQL-92) sono definiti in termini di questi fenomeni. Nella tabella seguente, una "X" contrassegna ogni fenomeno che può verificarsi.  
  
|Livello di isolamento delle transazioni|Letture sporche|Letture non ripetibili|Fantasmi|  
|---------------------------------|-----------------|-------------------------|--------------|  
|Read Uncommitted|X|X|X|  
|Read Committed|--|X|X|  
|Repeatable Read|--|--|X|  
|Serializable|--|--|--|  
  
 Nella tabella seguente vengono descritti semplici modi in cui un DBMS potrebbe implementare i livelli di isolamento delle transazioni.  
  
> [!IMPORTANT]  
>  La maggior parte dei DBS utilizza schemi più complessi di questi per aumentare la concorrenza. Questi esempi sono forniti solo a scopo illustrativo. In particolare, ODBC non prescrive il modo in cui particolari DBSMO isolano le transazioni l'una dall'altra.  
  
|Isolamento delle transazioni|Possibile attuazione|  
|---------------------------|-----------------------------|  
|Read Uncommitted|Le transazioni non sono isolate l'una dall'altra. Se il DBMS supporta altri livelli di isolamento delle transazioni, ignora qualsiasi meccanismo utilizzato per implementare tali livelli. In modo che non influiscano negativamente su altre transazioni, le transazioni in esecuzione a livello di lettura di cui non è stato eseguito il commit sono in genere di sola lettura.|  
|Read Committed|La transazione attende fino a quando le righe write-locked da altre transazioni vengono sbloccate; questo impedisce di leggere i dati "sporchi".<br /><br /> La transazione contiene un blocco di lettura (se legge solo la riga) o un blocco in scrittura (se aggiorna o elimina la riga) nella riga corrente per impedire ad altre transazioni di aggiornarla o eliminarla. La transazione rilascia blocchi di lettura quando si sposta all'estaso dalla riga corrente. Contiene blocchi di scrittura fino a quando non viene eseguito il commit o il rollback.|  
|Repeatable Read|La transazione attende fino a quando le righe write-locked da altre transazioni vengono sbloccate; questo impedisce di leggere i dati "sporchi".<br /><br /> La transazione contiene blocchi di lettura su tutte le righe restituite all'applicazione e blocchi di scrittura su tutte le righe inserite, aggiornate o eliminate. Ad esempio, se la transazione include l'istruzione SQL **SELECT \* FROM Orders**, la transazione blocca le righe durante il recupero da parte dell'applicazione. Se la transazione include l'istruzione SQL **DELETE FROM Orders WHERE Status - 'CLOSED'**, la transazione blocca le righe man mano che vengono eliminate.<br /><br /> Poiché altre transazioni non possono aggiornare o eliminare queste righe, la transazione corrente evita letture non ripetibili. La transazione rilascia i blocchi quando ne viene eseguito il commit o il rollback.|  
|Serializable|La transazione attende fino a quando le righe write-locked da altre transazioni vengono sbloccate; questo impedisce di leggere i dati "sporchi".<br /><br /> La transazione contiene un blocco di lettura (se legge solo le righe) o un blocco in scrittura (se è possibile aggiornare o eliminare righe) nell'intervallo di righe su cui ha effetto. Ad esempio, se la transazione include l'istruzione SQL **SELECT \* FROM Orders**, l'intervallo è l'intera tabella Orders; la transazione blocca la tabella e non consente l'inserimento di nuove righe. Se la transazione include l'istruzione SQL **DELETE FROM Orders WHERE Status : 'CLOSED'**, l'intervallo è costituito da tutte le righe con stato "CLOSED"; la transazione blocca tutte le righe della tabella Orders con stato "CLOSED" e non consente l'inserimento o l'aggiornamento di alcuna riga in modo che lo stato della riga risultante sia "CLOSED".<br /><br /> Poiché altre transazioni non possono aggiornare o eliminare le righe nell'intervallo, la transazione corrente evita letture non ripetibili. Poiché altre transazioni non possono inserire righe nell'intervallo, la transazione corrente evita qualsiasi fantasma. La transazione rilascia il blocco quando ne viene eseguito il commit o il rollback.|  
  
 È importante notare che il livello di isolamento della transazione non influisce sulla capacità di una transazione di visualizzare le proprie modifiche; le transazioni possono sempre vedere le modifiche apportate. Ad esempio, una transazione può essere costituita da due istruzioni **UPDATE,** la prima delle quali aumenta la retribuzione di tutti i dipendenti del 10% e la seconda imposta la retribuzione di tutti i dipendenti su un importo massimo pari a tale importo. Questa operazione ha esito positivo come una singola transazione solo perché la seconda istruzione **UPDATE** può visualizzare i risultati della prima.
