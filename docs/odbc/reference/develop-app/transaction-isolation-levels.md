---
title: Livelli di isolamento delle transazioni | Microsoft Docs
ms.custom: ''
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
ms.openlocfilehash: 83197b1b487db6c52a8fe9b7a57dd6af55c33571
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985113"
---
# <a name="transaction-isolation-levels"></a>Livelli di isolamento delle transazioni
I *Livelli di isolamento delle transazioni* sono una misura dell'esito positivo dell'isolamento delle transazioni. In particolare, i livelli di isolamento delle transazioni vengono definiti dalla presenza o assenza dei seguenti fenomeni:  
  
-   **Letture dirty** Una *lettura dirty* si verifica quando una transazione legge dei dati che non sono ancora stati committati. Ad esempio, si supponga che transazione 1 aggiorni una riga. La transazione 2 legge la riga prima che transazione 1 committi l'aggiornamento. Se la transazione 1 esegue il rollback della modifica, la transazione 2 avrà letto dei dati che sono considerati mai esistiti.  
  
-   **Letture non ripetibili** Una *lettura non ripetibile* si verifica quando una transazione legge la stessa riga due volte, ma ottiene ogni volta dati diversi. Ad esempio, si supponga transazione 1 legga una riga. La transazione 2 aggiorni o elimini tale riga ed esegue il commit di update o delete. Se la transazione 1 consente di leggere nuovamente la riga, recupera i valori di riga diversi o scopre che la riga è stata eliminata.
  
-   **Righe fantasma** Una *riga fantasma* è una riga che corrisponde ai criteri di ricerca, ma non viene inizialmente visualizzata. Si supponga, ad esempio, che la transazione 1 legge un set di righe che soddisfano alcuni criteri di ricerca. La transazione 2 genera una nuova riga (tramite un aggiornamento o un'operazione di inserimento) che corrisponde ai criteri di ricerca della transazione 1. Se la transazione 1 riesegue l'istruzione che legge le righe, ottiene un diverso set di righe.
  
 I quattro livelli di isolamento (come definito da SQL-92) sono definiti in termini di questi fenomeni. Nella tabella seguente, una "X" contrassegna ogni fenomeno che può verificarsi.  
  
|Livello di isolamento delle transazioni|Letture dirty|Letture non ripetibili|Righe fantasma|  
|---------------------------------|-----------------|-------------------------|--------------|  
|Read Uncommitted|x|X|x|  
|Read Committed|--|x|x|  
|Repeatable Read|--|--|x|  
|Serializable|--|--|--|  
  
 La tabella seguente descrive modi semplici che un sistema DBMS potrebbe implementare livelli di isolamento delle transazioni.  
  
> [!IMPORTANT]  
>  La maggior parte dei DBMS consente di implementare schemi più complessi rispetto a questi per aumentare la concorrenza. Questi esempi vengono forniti solo a scopo illustrativo. In particolare, ODBC non prevede modalità specifico DBMS isolare le transazioni tra loro.  
  
|isolamento delle transazioni|Implementazione possibili|  
|---------------------------|-----------------------------|  
|Read Uncommitted|Le transazioni non sono isolate tra loro. Se il sistema DBMS supporta altri livelli di isolamento delle transazioni, ignora qualsiasi meccanismo viene utilizzato per implementare tali livelli. In modo da non influire negativamente su altre transazioni, le transazioni eseguite al livello Read Uncommitted sono in genere di sola lettura.|  
|Read Committed|La transazione attende fino a quando le righe bloccate scrittura da altre transazioni vengono sbloccate; Ciò evita la lettura di tutti i dati "dirty".<br /><br /> Transazione mantiene un blocco di lettura (se legge solo la riga) o di scrittura di blocco (se si aggiorna o si elimina la riga) nella riga corrente per impedire che altre transazioni l'aggiornamento o eliminazione. La transazione rilascia i blocchi in lettura quando si sposta dalla riga corrente. Contiene dei blocchi di scrittura fino a quando non è stato eseguito il commit o rollback.|  
|Repeatable Read|La transazione attende fino a quando le righe bloccate scrittura da altre transazioni vengono sbloccate; Ciò evita la lettura di tutti i dati "dirty".<br /><br /> La transazione mantiene i blocchi in lettura su tutte le righe che per i blocchi applicazione e di scrittura restituisce tutte le righe vengano inserimenti, aggiornamenti o eliminati. Ad esempio, se la transazione include l'istruzione SQL **selezionate \* FROM Orders**, i blocchi di lettura delle transazioni le righe come l'applicazione recupera li. Se la transazione include l'istruzione SQL **Elimina dagli ordini in cui lo stato = 'Chiuso'** , i blocchi di scrittura delle transazioni le righe come li elimina.<br /><br /> Dato che altre transazioni non possono aggiornare o eliminare queste righe, la transazione corrente evita le letture non ripetibili. La transazione rilascia i relativi blocchi quando viene eseguito il commit o rollback.|  
|Serializable|La transazione attende fino a quando le righe bloccate scrittura da altre transazioni vengono sbloccate; Ciò evita la lettura di tutti i dati "dirty".<br /><br /> La transazione mantiene un blocco di lettura (se legge solo righe) o il blocco di scrittura (se è possibile aggiornare o eliminare righe) dell'intervallo di righe interessa. Ad esempio, se la transazione include l'istruzione SQL **selezionate \* FROM Orders**, l'intervallo è l'intera tabella Orders; i blocchi delle transazioni read-la tabella e non non consentire nuove righe da inserire al suo interno. Se la transazione include l'istruzione SQL **Elimina dagli ordini in cui lo stato = 'Chiuso'** , l'intervallo è tutte le righe con lo stato di "CLOSED"; i blocchi di scrittura delle transazioni tutte le righe di ordini di tabella con lo stato "CLOSED" e non non Consenti tutte le righe da inserire o aggiornare in modo che la riga risulta ha lo stato "CLOSED".<br /><br /> Dato che altre transazioni non possono aggiornare o eliminare le righe nell'intervallo, la transazione corrente evita le letture non ripetibili. Poiché le altre transazioni non è possibile inserire tutte le righe nell'intervallo, la transazione corrente consente di evitare eventuali righe fantasma. La transazione rilascia il blocco quando viene eseguito il commit o rollback.|  
  
 È importante notare che il livello di isolamento delle transazioni non influisce sulla possibilità di una transazione per visualizzare il proprio modifiche; le transazioni possono visualizzare sempre delle modifiche apportate. Ad esempio, che potrebbe consistere in una transazione di due **UPDATE** istruzioni, il primo dei quali genera il pagamento di tutti i dipendenti del 10% e il secondo dei quali imposta il pagamento di tutti i dipendenti tramite alcuni quantità massima di tale quantità. Ciò ha esito positivo come una singola transazione solo perché la seconda **UPDATE** istruzione è possibile visualizzare i risultati del primo.
