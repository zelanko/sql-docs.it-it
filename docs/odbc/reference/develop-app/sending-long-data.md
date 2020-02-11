---
title: Invio di dati lunghi | Microsoft Docs
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
ms.openlocfilehash: acb4ff1637c1530527af88affaf437334596016b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094346"
---
# <a name="sending-long-data"></a>Invio di dati Long
I DBMS definiscono *dati* di tipo long come dati di tipo carattere o binario su una determinata dimensione, ad esempio 254 caratteri. Potrebbe non essere possibile archiviare un intero elemento di dati lunghi in memoria, ad esempio quando l'elemento rappresenta un documento di testo lungo o una bitmap. Poiché tali dati non possono essere archiviati in un singolo buffer, l'origine dati lo invia al driver in parti con **SQLPutData** quando viene eseguita l'istruzione. I parametri per i quali vengono inviati i dati in fase di esecuzione sono noti come *parametri data-at-execution*.  
  
> [!NOTE]  
>  Un'applicazione può effettivamente inviare qualsiasi tipo di dati in fase di esecuzione con **SQLPutData**, anche se in parti possono essere inviati solo dati di tipo carattere e binario. Tuttavia, se i dati sono sufficientemente piccoli da adattarsi a un singolo buffer, in genere non esiste alcun motivo per usare **SQLPutData**. È molto più semplice associare il buffer e consentire al driver di recuperare i dati dal buffer.  
  
 Per inviare dati in fase di esecuzione, l'applicazione esegue le azioni seguenti:  
  
1.  Passa un valore a 32 bit che identifica il parametro nell'argomento *ParameterValuePtr* in **SQLBindParameter** anziché passare l'indirizzo di un buffer. Questo valore non viene analizzato dal driver. Il codice verrà restituito all'applicazione in un secondo momento, quindi dovrebbe essere un elemento dell'applicazione. Ad esempio, potrebbe essere il numero del parametro o l'handle di un file contenente i dati.  
  
2.  Passa l'indirizzo di un buffer di lunghezza/indicatore nell'argomento *StrLen_or_IndPtr* di **SQLBindParameter**.  
  
3.  Archivia SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC (*length*) nel buffer di lunghezza/indicatore. Entrambi questi valori indicano al driver che i dati per il parametro verranno inviati con **SQLPutData**. SQL_LEN_DATA_AT_EXEC (*length*) viene utilizzato quando si inviano dati Long a un'origine dati che deve essere in grado di stabilire il numero di byte di dati lunghi da inviare in modo da poter preallocare lo spazio. Per determinare se un'origine dati richiede questo valore, l'applicazione chiama **SQLGetInfo** con l'opzione SQL_NEED_LONG_DATA_LEN. Tutti i driver devono supportare questa macro. Se per l'origine dati non è necessaria la lunghezza in byte, il driver può ignorarlo.  
  
4.  Chiama **SQLExecute** o **SQLExecDirect**. Il driver rileva che un buffer di lunghezza/indicatore contiene il valore SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC (*length*) e restituisce SQL_NEED_DATA come valore restituito della funzione.  
  
5.  Chiama **SQLParamData** in risposta al valore restituito SQL_NEED_DATA. Se è necessario inviare dati lunghi, **SQLParamData** restituisce SQL_NEED_DATA. Nel buffer a cui punta l'argomento *ValuePtrPtr* , il driver restituisce il valore che identifica il parametro data-at-execution. Se è presente più di un parametro data-at-execution, l'applicazione deve usare questo valore per determinare per quale parametro inviare i dati; il driver non deve richiedere i dati per i parametri data-at-execution in un ordine particolare.  
  
6.  Chiama **SQLPutData** per inviare i dati del parametro al driver. Se i dati dei parametri non rientrano in un singolo buffer, come spesso accade con i dati lunghi, l'applicazione chiama ripetutamente **SQLPutData** per inviare i dati in parti; è possibile riassemblare i dati al driver e all'origine dati. Se l'applicazione passa dati stringa con terminazione null, il driver o l'origine dati deve rimuovere il carattere di terminazione null come parte del processo di riassemblaggio.  
  
7.  Chiama di nuovo **SQLParamData** per indicare che ha inviato tutti i dati per il parametro. Se sono presenti parametri data-at-execution per i quali non sono stati inviati dati, il driver restituisce SQL_NEED_DATA e il valore che identifica il parametro successivo. l'applicazione torna al passaggio 6. Se i dati sono stati inviati per tutti i parametri data-at-execution, viene eseguita l'istruzione. **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO e può restituire qualsiasi valore restituito o diagnostica che **SQLExecute** o **SQLExecDirect** può restituire.  
  
 Quando **SQLExecute** o **SQLExecDirect** restituisce SQL_NEED_DATA e prima che i dati siano stati inviati completamente per l'ultimo parametro data-at-execution, l'istruzione è in uno stato dei dati necessario. Mentre un'istruzione è in uno stato di dati necessario, l'applicazione può chiamare solo **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**o **SQLGetDiagRec**; tutte le altre funzioni restituiscono SQLSTATE HY010 (errore della sequenza di funzioni). Se si chiama **SQLCancel** , l'esecuzione dell'istruzione viene annullata e restituita allo stato precedente. Per ulteriori informazioni, vedere [Appendice B: tabelle di transizione dello stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Per un esempio di invio di dati in fase di esecuzione, vedere la descrizione della funzione [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) .
