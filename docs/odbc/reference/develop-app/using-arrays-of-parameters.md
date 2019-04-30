---
title: Uso delle matrici di parametri | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ff4a76c38f04c7b9b12842ef800bc8a26a27ed9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312515"
---
# <a name="using-arrays-of-parameters"></a>Uso delle matrici di parametri
Usare matrici di parametri, l'applicazione chiama **SQLSetStmtAttr** con un *attributo* argomento di SQL_ATTR_PARAMSET_SIZE per specificare il numero di set di parametri. Viene chiamato **SQLSetStmtAttr** con un *attributo* argomento di SQL_ATTR_PARAMS_PROCESSED_PTR per specificare l'indirizzo di una variabile in cui il driver può restituire il numero di set di parametri elaborati, inclusi i set di errore. Viene chiamato **SQLSetStmtAttr** con un *attributo* argomento di SQL_ATTR_PARAM_STATUS_PTR in modo che punti a una matrice in cui si desidera ottenere informazioni sullo stato per ogni riga di valori di parametro. Il driver archivia questi indirizzi nella struttura che viene mantenuta per l'istruzione.  
  
> [!NOTE]  
>  In ODBC 2. *x*, **SQLParamOptions** è stato chiamato per specificare più valori per un parametro. In ODBC 3. *x*, la chiamata a **SQLParamOptions** è stato sostituito dalle chiamate a **SQLSetStmtAttr** per impostare gli attributi SQL_ATTR_PARAMSET_SIZE e SQL_ATTR_PARAMS_PROCESSED_ARRAY .  
  
 Prima di eseguire l'istruzione, l'applicazione imposta il valore di ogni elemento di ogni matrice associata. Quando viene eseguita l'istruzione, il driver utilizza le informazioni memorizzata per recuperare i valori dei parametri e inviarli all'origine dati; Se possibile, il driver deve inviare questi valori come matrici. Sebbene l'utilizzo di matrici di parametri ottimale viene implementata tramite l'istruzione SQL con tutti i parametri nella matrice con una singola chiamata all'origine dati, questa funzionalità non è ampiamente disponibile in DBMS oggi stesso. Tuttavia, i driver possono simularla eseguendo un'istruzione SQL più volte, ognuna con un singolo set di parametri.  
  
 Prima di un'applicazione usa le matrici di parametri, è necessario assicurarsi che siano supportati dai driver usato dall'applicazione. Questa operazione può essere eseguita in due modi:  
  
-   Usare solo i driver supportano le matrici di parametri. L'applicazione può come hardcoded i nomi dei driver oppure è possibile indicare all'utente da usare solo questi driver. Applicazioni personalizzate e applicazioni verticali utilizzano comunemente un set limitato di driver.  
  
-   Verificare il supporto di matrici di parametri in fase di esecuzione. Un driver supporta matrici di parametri se è possibile impostare l'attributo di istruzione SQL_ATTR_PARAMSET_SIZE su un valore maggiore di 1. Applicazioni generiche e applicazioni verticali comunemente verificare il supporto di matrici di parametri in fase di esecuzione.  
  
 La disponibilità dei set di risultati in esecuzione con parametri e i conteggi delle righe può essere determinata chiamando **SQLGetInfo** con le opzioni SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS. Per **inserire**, **UPDATE**, e **eliminare** (istruzioni), l'opzione SQL_PARAM_ARRAY_ROW_COUNTS indica se i conteggi delle righe singole (uno per ogni set di parametri) disponibile (SQL_PARC_BATCH) o se i conteggi delle righe vengono raggruppate in un unico (SQL_PARC_NO_BATCH). Per la **seleziona** (istruzioni), l'opzione SQL_PARAM_ARRAY_SELECTS indica se un set di risultati è disponibile per ogni set di parametri (SQL_PAS_BATCH) o se solo un set di risultati è disponibile (SQL_PAS_NO_BATCH). Se il driver non supporta istruzioni che generano set di risultati deve essere eseguito con una matrice di parametri, SQL_PARAM_ARRAY_SELECTS restituisce SQL_PAS_NO_SELECT. Si tratta di dati specifici dell'origine se le matrici di parametri possono essere usate con altri tipi di istruzioni, soprattutto perché l'utilizzo di parametri in queste istruzioni sarebbe specifiche dell'origine dati e non seguirà la grammatica SQL ODBC.  
  
 La matrice a cui punta l'attributo di istruzione SQL_ATTR_PARAM_OPERATION_PTR può essere utilizzata per ignorare le righe di parametri. Se un elemento della matrice è impostato su SQL_PARAM_IGNORE, il set di parametri corrisponde a tale elemento è escluso dal **SQLExecute** oppure **SQLExecDirect** chiamare. La matrice a cui punta l'attributo SQL_ATTR_PARAM_OPERATION_PTR viene allocata e compilata dall'applicazione e letti dal driver. Se righe recuperate vengono usate come parametri di input, i valori della matrice di stato di riga possono essere usati nella matrice di operazione del parametro.  
  
## <a name="error-processing"></a>Errore di elaborazione  
 Se si verifica un errore durante l'esecuzione dell'istruzione, la funzione di esecuzione restituisce un errore e imposta la variabile di numeri di riga per il numero della riga contenente l'errore. Si tratta di dati specifici dell'origine se tutte le righe ad eccezione del fatto venga eseguito il set di errore o se tutte le righe prima (ma non dopo) vengono eseguiti il caso di errore impostato. Poiché l'elaborazione di set di parametri, il driver imposta il buffer specificato dall'attributo di istruzione SQL_ATTR_PARAMS_PROCESSED_PTR per il numero di riga in fase di elaborazione. Se tutti i set, ad eccezione del fatto che vengono eseguiti il caso di errore impostato, il driver imposta questo buffer a SQL_ATTR_PARAMSET_SIZE dopo che tutte le righe vengono elaborate.  
  
 Se è stato impostato l'attributo di istruzione SQL_ATTR_PARAM_STATUS_PTR, **SQLExecute** oppure **SQLExecDirect** restituisce il *matrice di stato* che fornisce lo stato di ogni set di parametri. Matrice di stato del parametro viene allocata dall'applicazione e compilata dal driver. Gli elementi indicano se l'istruzione SQL è stata eseguita correttamente per la riga di parametri o se si è verificato un errore durante l'elaborazione di set di parametri. Se si è verificato un errore, il driver imposta il valore corrispondente nella matrice di stato del parametro a SQL_PARAM_ERROR e viene restituito SQL_SUCCESS_WITH_INFO. L'applicazione può verificare la matrice di stati per determinare quali righe sono state elaborate. Utilizzando il numero di riga, l'applicazione può spesso risolvere l'errore e riprendere l'elaborazione.  
  
 Come matrice di stato del parametro viene usata è determinata dalle opzioni di SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS restituite da una chiamata a **SQLGetInfo**. Per la **inserire**, **UPDATE**, e **eliminare** (istruzioni), la matrice di stati di parametro vengono inserite le informazioni sullo stato se SQL_PARC_BATCH viene restituito per SQL_PARAM_ARRAY_ ROW_COUNTS, ma non in SQL_PARC_NO_BATCH viene restituito. Per la **seleziona** (istruzioni), la matrice di stato del parametro viene compilata SQL_PAS_BATCH viene restituita per SQL_PARAM_ARRAY_SELECT, ma non viene restituito SQL_PAS_NO_BATCH o SQL_PAS_NO_SELECT.  
  
## <a name="data-at-execution-parameters"></a>Parametri data-at-Execution  
 Se uno qualsiasi dei valori nella matrice di lunghezza/indicatore SQL_DATA_AT_EXEC o il risultato di SQL_LEN_DATA_AT_EXEC (*lunghezza*) (macro), i dati per tali valori vengono inviati con **SQLPutData** nel modo consueto. I seguenti aspetti di questo processo tenere commento speciale perché non sono proprio ovvie:  
  
-   Quando il driver restituisce SQL_NEED_DATA, è necessario impostare l'indirizzo della variabile di numeri di riga alla riga per cui necessita di dati. Come nel caso a valore singolo, l'applicazione non può fare supposizioni relative all'ordine in cui il driver richiederà i valori dei parametri all'interno di un singolo set di parametri. Se si verifica un errore nell'esecuzione di un parametro data-at-execution, il buffer specificato dall'attributo di istruzione SQL_ATTR_PARAMS_PROCESSED_PTR viene impostato sul numero di riga in cui l'errore si è verificato, lo stato per la riga nella matrice di stato di riga specificata da l'attributo di istruzione SQL_ATTR_PARAM_STATUS_PTR è impostato su SQL_PARAM_ERROR e la chiamata a **SQLExecute**, **SQLExecDirect**, **SQLParamData**, o  **SQLPutData** restituisce SQL_ERROR. Il contenuto di questo buffer è indefinito se **SQLExecute**, **SQLExecDirect**, o **SQLParamData** restituire SQL_STILL_EXECUTING.  
  
-   Poiché il driver non interpreta il valore di *ParameterValuePtr* argomento di **SQLBindParameter** per i parametri data-at-execution, se l'applicazione fornisce un puntatore a una matrice,  **SQLParamData** non estrarre e restituire un elemento di questa matrice per l'applicazione. Al contrario, restituisce che il valore scalare l'applicazione ha fornito. Ciò significa che il valore restituito da **SQLParamData** è non è sufficiente specificare il parametro per il quale l'applicazione deve inviare i dati, l'applicazione deve inoltre prendere in considerazione il numero di riga corrente.  
  
     Quando solo alcuni degli elementi della matrice di parametri sono parametri data-at-execution, l'applicazione deve passare l'indirizzo di una matrice nel *ParameterValuePtr* che contiene gli elementi per tutti i parametri. Questa matrice viene interpretata in genere per i parametri che non sono parametri data-at-execution. Per i parametri data-at-execution, il valore che **SQLParamData** fornisce per l'applicazione, che in genere può essere usato per identificare i dati che richiede il driver in questa occasione, è sempre l'indirizzo della matrice.
