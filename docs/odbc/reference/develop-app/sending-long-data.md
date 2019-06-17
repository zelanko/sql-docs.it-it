---
title: Invio di dati Long | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc7a140d7de8548f02fde6ab309823bbe1c9c656
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62465927"
---
# <a name="sending-long-data"></a>Invio di dati Long
Definiscono DBMS *dati di tipo long* come qualsiasi carattere o dati binari in una determinata dimensione, ad esempio di 254 caratteri. Potrebbe non essere possibile archiviare l'intero elemento di dati long in memoria, ad esempio quando l'elemento rappresenta un documento di testo lungo o in una bitmap. Perché questo tipo di dati non può essere archiviati in un singolo buffer, lo invia al driver in parti con l'origine dati **SQLPutData** quando viene eseguita l'istruzione. I parametri per il quale i dati vengono inviati in fase di esecuzione sono noti come *parametri data-at-execution*.  
  
> [!NOTE]  
>  Un'applicazione può inviare effettivamente i dati di qualsiasi tipo in fase di esecuzione con **SQLPutData**, anche se solo i caratteri e dati binari possono essere inviati in parti. Tuttavia, se i dati sono sufficientemente piccoli da rientrare in un singolo buffer, non è in genere necessario usare **SQLPutData**. È molto più semplice associare il buffer e lasciare che il driver di recuperare i dati dal buffer.  
  
 Per inviare dati in fase di esecuzione, l'applicazione esegue le azioni seguenti:  
  
1.  Passa un valore a 32 bit che identifica il parametro nel *ParameterValuePtr* nell'argomento **SQLBindParameter** invece di passare l'indirizzo di un buffer. Questo valore non viene analizzato dal driver. Verrà restituito all'applicazione in un secondo momento, in modo che indicano un elemento all'applicazione. Ad esempio, potrebbe essere il numero del parametro o l'handle di un file contenente i dati.  
  
2.  Passa l'indirizzo di un buffer di lunghezza/indicatore nel *StrLen_or_IndPtr* argomenti del **SQLBindParameter**.  
  
3.  Archivia SQL_DATA_AT_EXEC o il risultato di SQL_LEN_DATA_AT_EXEC (*lunghezza*) (macro) nel buffer di lunghezza/indicatore. Entrambi questi valori indicano al driver che verranno inviati con i dati per il parametro **SQLPutData**. SQL_LEN_DATA_AT_EXEC (*lunghezza*) viene usato quando si inviano dati di tipo long a un'origine dati che deve conoscere il numero di byte di dati long verrà inviato in modo che può preallocare lo spazio. Per determinare se un'origine dati richiede questo valore, l'applicazione chiama **SQLGetInfo** con l'opzione SQL_NEED_LONG_DATA_LEN. Tutti i driver devono supportare questa macro. Se l'origine dati non richiede la lunghezza in byte, il driver può ignorarlo.  
  
4.  Le chiamate **SQLExecute** oppure **SQLExecDirect**. Il driver individua che un buffer di lunghezza/indicatore che contiene il valore SQL_DATA_AT_EXEC o il risultato di SQL_LEN_DATA_AT_EXEC (*lunghezza*) restituisce SQL_NEED_DATA come valore restituito della funzione e macro.  
  
5.  Le chiamate **SQLParamData** in risposta a SQL_NEED_DATA il valore restituito. Se devono essere inviato, dati di tipo long **SQLParamData** restituisce SQL_NEED_DATA. Nel buffer a cui fa riferimento il *ValuePtrPtr* argomento, il driver restituisce il valore che identifica il parametro data-at-execution. Se è presente più di un parametro data-at-execution, l'applicazione deve usare questo valore per determinare quale parametro per inviare i dati; il driver non è necessario per richiedere i dati per i parametri data-at-execution in un ordine particolare.  
  
6.  Le chiamate **SQLPutData** per inviare i dati dei parametri al driver. Se i dati del parametro non rientrano in un singolo buffer, come accade spesso con dati di tipo long, l'applicazione chiama **SQLPutData** ripetutamente per inviare i dati in parti; in questo caso, il driver e l'origine dati per riassemblare i dati. Se l'applicazione passa i dati di stringa a terminazione null, l'origine dati o driver necessario rimuovere il carattere di terminazione null come parte del processo di riassemblaggio.  
  
7.  Le chiamate **SQLParamData** nuovamente per indicare che è stato inviato a tutti i dati per il parametro. Se sono presenti parametri data-at-execution per i quali non sono stati inviati i dati, il driver restituisce SQL_NEED_DATA e il valore che identifica il parametro successivo. l'applicazione torna al passaggio 6. Se i dati sono stati inviati per tutti i parametri data-at-execution, viene eseguita l'istruzione. **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO e può restituiscono qualsiasi valore restituito o diagnostica che **SQLExecute** oppure **SQLExecDirect** può restituire.  
  
 Dopo aver **SQLExecute** oppure **SQLExecDirect** restituisce SQL_NEED_DATA e prima che i dati sono stati inviati completamente per l'ultimo parametro data-at-execution, l'istruzione si trova in uno stato necessario dei dati. Mentre un'istruzione è in uno stato necessario dei dati, l'applicazione può chiamare solo **SQLPutData**, **SQLParamData**, **SQLCancel**, **funzione SQLGetDiagField**, oppure **SQLGetDiagRec**; tutte le altre funzioni restituiscono SQLSTATE HY010 (funzione di errore nella sequenza). La chiamata **SQLCancel** Annulla l'esecuzione dell'istruzione e lo restituisce lo stato precedente. Per altre informazioni, vedere [appendice b: Tabelle della transizione di stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Per un esempio di invio dei dati in fase di esecuzione, vedere la [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) descrizione della funzione.
