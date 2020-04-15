---
title: Proprietà Alignment . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 205cc3ff95dd60db215150f46ae894fbb99bd9ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288606"
---
# <a name="alignment"></a>Alignment
I problemi di allineamento in un'applicazione ODBC non sono in genere diversi da quelli presenti in qualsiasi altra applicazione. Ovvero, la maggior parte delle applicazioni ODBC hanno pochi o nessun problema con l'allineamento. Le sanzioni per non allineare gli indirizzi variano con l'hardware e il sistema operativo e potrebbero essere minori come una leggera riduzione delle prestazioni o gravi come un errore di run-time fatale. Pertanto, le applicazioni ODBC e le applicazioni ODBC portabili in particolare, devono fare attenzione ad allineare i dati correttamente.  
  
 Un esempio di quando le applicazioni ODBC riscontrano problemi di allineamento è quando allocano un blocco di memoria di grandi dimensioni e associano parti diverse di tale memoria alle colonne in un set di risultati. Ciò si verifica con maggiore probabilità quando un'applicazione generica deve determinare la forma di un set di risultati in fase di esecuzione e allocare e associare la memoria di conseguenza.  
  
 Si supponga, ad esempio, che un'applicazione esegua un'istruzione **SELECT** immessa dall'utente e recuperi i risultati da questa istruzione. Poiché la forma di questo set di risultati non è nota quando viene scritto il programma, l'applicazione deve determinare il tipo di ogni colonna dopo la creazione del set di risultati e associare la memoria di conseguenza. Il modo più semplice per eseguire questa operazione consiste nell'allocare un blocco di memoria di grandi dimensioni e associare indirizzi diversi in tale blocco a ogni colonna. Per accedere ai dati in una colonna, l'applicazione esegue il cast della memoria associata a tale colonna.  
  
 Nel diagramma seguente viene illustrato un set di risultati di esempio e come un blocco di memoria potrebbe essere associato utilizzando il tipo di dati C predefinito per ogni tipo di dati SQL. Ogni "X" rappresenta un singolo byte di memoria. (Questo esempio mostra solo i buffer di dati associati alle colonne. Questo viene fatto per semplicità. Nel codice effettivo, anche i buffer di lunghezza/indicatore devono essere allineati.)  
  
 ![Associazione tramite l'impostazione del tipo di dati SQL come predefinito per il tipo di dati C](../../../odbc/reference/develop-app/media/pr24.gif "pr24 (informazioni in base alle proprietà del")  
  
 Supponendo che gli indirizzi associati siano archiviati nella matrice *Address,* l'applicazione utilizza le espressioni seguenti per accedere alla memoria associata a ogni colonna:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 Si noti che gli indirizzi associati alla seconda e alla terza colonna iniziano con i byte dispari e che l'indirizzo associato alla terza colonna non è divisibile per quattro, ovvero la dimensione di un File SDWORD. Su alcune macchine, questo non sarà un problema; su altri, causerà una leggera penalizzazione delle prestazioni; su altri ancora, causerà un errore di run-time fatale. Una soluzione migliore potrebbe essere quella di allineare ogni indirizzo associato sul suo limite di allineamento naturale. Supponendo che questo sia 1 per un UCHAR, 2 per un SWORD e 4 per un SDWORD, questo darebbe il risultato mostrato nella figura seguente, dove una "X" rappresenta un byte di memoria che viene utilizzato e una "O" rappresenta un byte di memoria che è inutilizzato.  
  
 ![Associazione tramite limite di allineamento naturale](../../../odbc/reference/develop-app/media/pr25.gif "pr25 (informazioni in stato di pr25")  
  
 Sebbene questa soluzione non utilizzi tutta la memoria dell'applicazione, non riscontra problemi di allineamento. Sfortunatamente, è necessaria una discreta quantità di codice per implementare questa soluzione, poiché ogni colonna deve essere allineata singolarmente in base al tipo. Una soluzione più semplice consiste nell'allineare tutte le colonne sulla dimensione del limite di allineamento più grande, ovvero 4 nell'esempio illustrato nella figura seguente.  
  
 ![Associazione tramite limite di allineamento massimo](../../../odbc/reference/develop-app/media/pr26.gif "pr26 (informazioni in inglese)")  
  
 Anche se questa soluzione lascia fori più grandi, il codice per implementarlo è relativamente semplice e veloce. Nella maggior parte dei casi, questo compensa la penalità pagata in memoria inutilizzata. Per un esempio in cui viene utilizzato questo metodo, vedere [Utilizzo di SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).
