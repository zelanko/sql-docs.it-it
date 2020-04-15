---
title: Invio di dati long Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aeeeb716aa2f9a72338f3aeb586dffce86f84069
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304182"
---
# <a name="sending-long-data"></a>Invio di dati Long
I DBS definiscono i *dati long* come qualsiasi carattere o dati binari di una determinata dimensione, ad esempio 254 caratteri. Potrebbe non essere possibile archiviare un intero elemento di dati lunghi in memoria, ad esempio quando l'elemento rappresenta un documento di testo lungo o una bitmap. Poiché tali dati non possono essere archiviati in un singolo buffer, l'origine dati li invia al driver in parti con **SQLPutData** quando viene eseguita l'istruzione. I parametri per i quali i dati vengono inviati in fase di esecuzione sono noti come *parametri data-at-execution*.  
  
> [!NOTE]  
>  Un'applicazione può effettivamente inviare qualsiasi tipo di dati in fase di esecuzione con **SQLPutData**, anche se solo i dati di tipo carattere e binario possono essere inviati in parti. Tuttavia, se i dati sono sufficientemente piccoli da essere contenuti in un singolo buffer, non vi è in genere alcun motivo per utilizzare **SQLPutData**. È molto più semplice associare il buffer e consentire al driver di recuperare i dati dal buffer.  
  
 Per inviare dati in fase di esecuzione, l'applicazione esegue le azioni seguenti:To send data at execution time, the application performs the following actions:  
  
1.  Passa un valore a 32 bit che identifica il parametro nell'argomento *ParameterValuePtr* in **SQLBindParameter** anziché passare l'indirizzo di un buffer. Questo valore non viene analizzato dal driver. Verrà restituito all'applicazione in un secondo momento, pertanto dovrebbe significare qualcosa per l'applicazione. Ad esempio, potrebbe essere il numero del parametro o l'handle di un file contenente dati.  
  
2.  Passa l'indirizzo di un buffer di lunghezza/indicatore nel *StrLen_or_IndPtr* argomento di **SQLBindParameter**.  
  
3.  Memorizza SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC(*length*) nel buffer di lunghezza/indicatore. Entrambi questi valori indicano al driver che i dati per il parametro verranno inviati con **SQLPutData**. SQL_LEN_DATA_AT_EXEC(*length*) viene utilizzato quando si inviano dati lunghi a un'origine dati che deve sapere quanti byte di dati long verranno inviati in modo da poter preallocare spazio. Per determinare se un'origine dati richiede questo valore, l'applicazione chiama **SQLGetInfo** con l'opzione SQL_NEED_LONG_DATA_LEN. Tutti i driver devono supportare questa macro; Se l'origine dati non richiede la lunghezza in byte, il driver può ignorarla.  
  
4.  Chiama **SQLExecute** o **SQLExecDirect**. Il driver rileva che un buffer di lunghezza/indicatore contiene il valore SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC(*length*) e restituisce SQL_NEED_DATA come valore restituito della funzione.  
  
5.  Chiama **SQLParamData** in risposta al valore restituito SQL_NEED_DATA. Se è necessario inviare dati lunghi, **SQLParamData** restituisce SQL_NEED_DATA. Nel buffer a cui punta l'argomento *ValuePtrPtr,* il driver restituisce il valore che identifica il parametro data-at-execution. Se è presente più di un parametro data-at-execution, l'applicazione deve utilizzare questo valore per determinare il parametro per cui inviare i dati. il driver non è tenuto a richiedere dati per i parametri data-at-execution in un ordine particolare.  
  
6.  Chiama **SQLPutData** per inviare i dati dei parametri al driver. Se i dati del parametro non rientrano in un singolo buffer, come spesso accade con i dati lunghi, l'applicazione chiama **SQLPutData** ripetutamente per inviare i dati in parti; spetta al driver e all'origine dati riassemblare i dati. Se l'applicazione passa dati stringa con terminazione null, il driver o l'origine dati deve rimuovere il carattere di terminazione null come parte del processo di riassemblaggio.  
  
7.  Chiama nuovamente **SQLParamData** per indicare che ha inviato tutti i dati per il parametro. Se sono presenti parametri data-at-execution per i quali i dati non sono stati inviati, il driver restituisce SQL_NEED_DATA e il valore che identifica il parametro successivo; l'applicazione torna al passaggio 6. Se sono stati inviati dati per tutti i parametri data-at-execution, l'istruzione viene eseguita. **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO e può restituire qualsiasi valore restituito o diagnostica che **SQLExecute** o **SQLExecDirect** può restituire.  
  
 Dopo **che SQLExecute** o **SQLExecDirect** restituisce SQL_NEED_DATA e prima che i dati siano stati inviati completamente per l'ultimo parametro data-at-execution, l'istruzione si trova in uno stato di dati necessari. Mentre un'istruzione si trova nello stato Need Data, l'applicazione può chiamare solo **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**o **SQLGetDiagRec**; tutte le altre funzioni restituiscono SQLSTATE HY010 (errore di sequenza di funzione). La chiamata a **SQLCancel** annulla l'esecuzione dell'istruzione e la riporta allo stato precedente. Per ulteriori informazioni, vedere [Appendice B: tabelle](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)di transizione dello stato ODBC .  
  
 Per un esempio di invio di dati in fase di esecuzione, vedere la descrizione della funzione [SQLPutData.For](../../../odbc/reference/syntax/sqlputdata-function.md) an example of sending data at execution time, see the SQLPutData function description.
