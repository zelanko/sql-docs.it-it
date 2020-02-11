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
ms.openlocfilehash: b8b5a107f5ed8cd1c6c45317e60cc515a2601316
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077274"
---
# <a name="alignment"></a>Alignment
I problemi di allineamento in un'applicazione ODBC non sono in genere diversi da quelli presenti in altre applicazioni. Ovvero, la maggior parte delle applicazioni ODBC presenta pochi o nessun problema di allineamento. Le sanzioni per la mancata allineatura degli indirizzi variano a seconda dell'hardware e del sistema operativo e potrebbero essere meno lievi come una lieve riduzione delle prestazioni o come un errore irreversibile in fase di esecuzione. Pertanto, le applicazioni ODBC e le applicazioni ODBC portabili, in particolare, devono prestare attenzione a allineare correttamente i dati.  
  
 Un esempio di quando le applicazioni ODBC rilevano problemi di allineamento si verifica quando allocano un blocco di memoria di grandi dimensioni e associano parti diverse di tale memoria alle colonne di un set di risultati. Questa situazione si verifica con maggiore probabilità quando un'applicazione generica deve determinare la forma di un set di risultati in fase di esecuzione e allocare e associare la memoria di conseguenza.  
  
 Si supponga, ad esempio, che un'applicazione esegua un'istruzione **Select** immessa dall'utente e recuperi i risultati restituiti da questa istruzione. Poiché la forma di questo set di risultati non è nota quando viene scritto il programma, l'applicazione deve determinare il tipo di ogni colonna dopo che il set di risultati è stato creato e associare di conseguenza la memoria. Il modo più semplice per eseguire questa operazione consiste nell'allocare un blocco di memoria di grandi dimensioni e associare indirizzi diversi in tale blocco a ogni colonna. Per accedere ai dati in una colonna, l'applicazione esegue il cast della memoria associata a tale colonna.  
  
 Il diagramma seguente illustra un set di risultati di esempio e il modo in cui un blocco di memoria può essere associato usando il tipo di dati C predefinito per ogni tipo di dati SQL. Ogni "X" rappresenta un singolo byte di memoria. In questo esempio vengono mostrati solo i buffer di dati associati alle colonne. Questa operazione viene eseguita per semplicità. Nel codice effettivo, i buffer di lunghezza/indicatore devono anche essere allineati.  
  
 ![Associazione tramite l'impostazione del tipo di dati SQL come predefinito per il tipo di dati C](../../../odbc/reference/develop-app/media/pr24.gif "PR24")  
  
 Supponendo che gli indirizzi associati siano archiviati nella matrice di *indirizzi* , l'applicazione usa le espressioni seguenti per accedere alla memoria associata a ogni colonna:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 Si noti che gli indirizzi associati alla seconda e terza colonna iniziano in byte dispari e che l'indirizzo associato alla terza colonna non è divisibile per quattro, ovvero la dimensione di un SDWORD. In alcuni computer, non si tratta di un problema; in altri casi, si verificherà una lieve riduzione delle prestazioni. in altri ancora, verrà generato un errore irreversibile in fase di esecuzione. Una soluzione migliore consiste nell'allineare ogni indirizzo associato al limite di allineamento naturale. Supponendo che sia 1 per UCHAR, 2 per una spada e 4 per un SDWORD, questo darebbe il risultato illustrato nella figura seguente, in cui una "X" rappresenta un byte di memoria usato e un "O" rappresenta un byte di memoria inutilizzato.  
  
 ![Associazione tramite limite di allineamento naturale](../../../odbc/reference/develop-app/media/pr25.gif "PR25")  
  
 Sebbene questa soluzione non utilizzi tutta la memoria dell'applicazione, non si verificano problemi di allineamento. Sfortunatamente, richiede una notevole quantità di codice per implementare questa soluzione, perché ogni colonna deve essere allineata singolarmente in base al tipo. Una soluzione più semplice consiste nell'allineare tutte le colonne sulle dimensioni del limite di allineamento più grande, ovvero 4 nell'esempio illustrato nella figura seguente.  
  
 ![Associazione tramite limite di allineamento massimo](../../../odbc/reference/develop-app/media/pr26.gif "PR26")  
  
 Sebbene questa soluzione lasci più buchi, il codice per implementarlo è relativamente semplice e veloce. Nella maggior parte dei casi, questo compensa la penalità pagata nella memoria inutilizzata. Per un esempio che usa questo metodo, vedere [uso di SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).
