---
title: Allineamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alignment issues [ODBC]
ms.assetid: 06a01e51-e7a5-495f-aa27-e304b0d005ff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e4c86fd8fba66e6424b41fa4b80b42fc089e6d64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287461"
---
# <a name="alignment"></a>Allineamento
I problemi di allineamento in un'applicazione ODBC a livello generale non sono diversi rispetto a qualsiasi altra applicazione. Vale a dire, la maggior parte delle applicazioni ODBC capita pochi o Nessun allineamento. Le sanzioni per l'allineamento non indirizzi variano con l'hardware e sistema operativo e potrebbero essere come principale come un errore irreversibile in fase di esecuzione o come secondaria come una riduzione delle prestazioni leggero. Pertanto, le applicazioni ODBC e le applicazioni ODBC portabile, in particolare, devono prestare attenzione per i dati sono allineati correttamente.  
  
 Un esempio di quando le applicazioni ODBC si verifichino problemi di allineamento è quando si alloca un blocco di memoria di grandi dimensioni e associare diverse parti di tale memoria per le colonne in un set di risultati. Si tratta probabilmente si verifica quando un'applicazione generica deve determinare la forma di un set di risultati in fase di esecuzione e allocare e associare memoria di conseguenza.  
  
 Ad esempio, si supponga che un'applicazione esegue una **seleziona** istruzione immesso dall'utente e recupera i risultati ottenuti con questa istruzione. Poiché la forma di questo set di risultati non è noto quando viene scritto il programma, l'applicazione deve determinare il tipo di ogni colonna dopo aver creato il set di risultati e associare memoria di conseguenza. Il modo più semplice per eseguire questa operazione è per allocare un blocco di memoria di grandi dimensioni e associare diversi indirizzi in blocco per ogni colonna. Per accedere ai dati in una colonna, l'applicazione esegue il cast della memoria associata a tale colonna.  
  
 Il diagramma seguente mostra un esempio di risultato, impostare e come un blocco di memoria potrebbe essere associato, utilizzando il tipo di dati C predefiniti per ogni tipo di dati SQL. Ogni "X" rappresenta un singolo byte di memoria. (Questo esempio mostra solo i buffer di dati che sono associati alle colonne. Questa operazione viene eseguita per motivi di semplicità. Nel codice effettivo, i buffer di lunghezza/indicatore devono inoltre essere allineati.)  
  
 ![Associazione tramite il tipo di dati C predefinito al tipo di dati SQL](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 Supponendo che gli indirizzi associati vengono archiviati nel *indirizzo* matrice, l'applicazione usa le espressioni seguenti per accedere alla memoria associata a ogni colonna:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 Si noti che gli indirizzi associati al secondo e terzo colonne avviare in byte dispari e che l'indirizzo associato alla terza colonna non è divisibile per quattro elementi, ovvero le dimensioni di un SDWORD. In alcuni computer, si tratta di un problema. altri utenti, ciò comporterà una riduzione delle prestazioni leggermente migliori; comunque altri utenti, causerà un errore irreversibile in fase di esecuzione. Una soluzione migliore sarebbe per allineare ogni indirizzo associato nel relativo limite di allineamento naturale. Supponendo che si tratta di 1 per un UCHAR, per una sua spada per il 2 e 4 per un SDWORD, si otterrebbero i risultati illustrato nella figura seguente, in cui una "X" rappresenta un byte di memoria utilizzata e un'operazione "O" rappresenta un byte di memoria inutilizzata.  
  
 ![Associazione tramite limite di allineamento naturale](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 Sebbene questa soluzione non usa tutta la memoria dell'applicazione, eventuali problemi di allineamento non viene rilevato. Sfortunatamente, richiede una notevole quantità di codice per implementare questa soluzione, ogni colonna deve essere allineato singolarmente in base al relativo tipo. Una soluzione più semplice è sufficiente allineare tutte le colonne sulla dimensione del limite di allineamento massimo, ovvero 4 nell'esempio illustrato nella figura seguente.  
  
 ![Associazione tramite limite di allineamento massimo](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 Sebbene questa soluzione lascia aree libere di dimensioni maggiori, il codice per l'implementazione è relativamente semplice e veloce. Nella maggior parte dei casi, questo viene eseguito l'offset la penalità pagata in memoria inutilizzata. Per un esempio che usa questo metodo, vedere [SQLBindCol usando](../../../odbc/reference/develop-app/using-sqlbindcol.md).
