---
title: Uso di matrici di parametri | Microsoft Docs
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
ms.openlocfilehash: cf6b5127bac7aedf9e67918d38020c73a4afe186
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68079606"
---
# <a name="using-arrays-of-parameters"></a>Uso delle matrici di parametri
Per usare matrici di parametri, l'applicazione chiama **SQLSetStmtAttr** con un argomento *attribute* di SQL_ATTR_PARAMSET_SIZE per specificare il numero di set di parametri. Chiama **SQLSetStmtAttr** con un argomento *attribute* di SQL_ATTR_PARAMS_PROCESSED_PTR per specificare l'indirizzo di una variabile in cui il driver può restituire il numero di set di parametri elaborati, inclusi i set di errori. Chiama **SQLSetStmtAttr** con un argomento *attribute* di SQL_ATTR_PARAM_STATUS_PTR per puntare a una matrice in cui restituire informazioni sullo stato per ogni riga di valori di parametro. Il driver archivia questi indirizzi nella struttura che gestisce per l'istruzione.  
  
> [!NOTE]  
>  In ODBC 2. *x*, **SQLParamOptions** è stato chiamato per specificare più valori per un parametro. In ODBC 3. *x*, la chiamata a **SQLParamOptions** è stata sostituita dalle chiamate a **SQLSetStmtAttr** per impostare gli attributi SQL_ATTR_PARAMSET_SIZE e SQL_ATTR_PARAMS_PROCESSED_ARRAY.  
  
 Prima di eseguire l'istruzione, l'applicazione imposta il valore di ogni elemento di ogni matrice associata. Quando l'istruzione viene eseguita, il driver utilizza le informazioni archiviate per recuperare i valori dei parametri e inviarli all'origine dati. Se possibile, il driver deve inviare questi valori come matrici. Sebbene l'utilizzo di matrici di parametri venga implementato in modo ottimale eseguendo l'istruzione SQL con tutti i parametri nella matrice con una singola chiamata all'origine dati, questa funzionalità non è attualmente disponibile nei sistemi DBMS. Tuttavia, i driver possono simularlo eseguendo un'istruzione SQL più volte, ognuna con un unico set di parametri.  
  
 Prima che un'applicazione utilizzi matrici di parametri, è necessario assicurarsi che siano supportate dai driver utilizzati dall'applicazione. A questo scopo è possibile procedere in due modi:  
  
-   Utilizzare solo i driver noti per supportare matrici di parametri. L'applicazione è in grado di impostare come hardcoded i nomi di questi driver oppure è possibile chiedere all'utente di usare solo questi driver. Le applicazioni personalizzate e le applicazioni verticali utilizzano in genere un set limitato di driver.  
  
-   Verificare il supporto di matrici di parametri in fase di esecuzione. Un driver supporta matrici di parametri se è possibile impostare l'attributo dell'istruzione SQL_ATTR_PARAMSET_SIZE su un valore maggiore di 1. Le applicazioni generiche e le applicazioni verticali controllano in genere il supporto di matrici di parametri in fase di esecuzione.  
  
 La disponibilità dei conteggi delle righe e dei set di risultati nell'esecuzione con parametri può essere determinata chiamando **SQLGetInfo** con le opzioni SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS. Per le istruzioni **Insert**, **Update**e **Delete** , l'opzione SQL_PARAM_ARRAY_ROW_COUNTS indica se i conteggi delle singole righe (uno per ogni set di parametri) sono disponibili (SQL_PARC_BATCH) o se viene eseguito il rollup dei conteggi delle righe in uno (SQL_PARC_NO_BATCH). Per le istruzioni **Select** , l'opzione SQL_PARAM_ARRAY_SELECTS indica se un set di risultati è disponibile per ogni set di parametri (SQL_PAS_BATCH) o se è disponibile un solo set di risultati (SQL_PAS_NO_BATCH). Se il driver non consente l'esecuzione di istruzioni di generazione dei set di risultati con una matrice di parametri, SQL_PARAM_ARRAY_SELECTS restituisce SQL_PAS_NO_SELECT. Si tratta di un'origine dati specifica se le matrici di parametri possono essere utilizzate con altri tipi di istruzioni, soprattutto perché l'utilizzo di parametri in queste istruzioni sarà specifico dell'origine dati e non seguirà la grammatica SQL ODBC.  
  
 La matrice a cui fa riferimento l'attributo dell'istruzione SQL_ATTR_PARAM_OPERATION_PTR può essere utilizzata per ignorare le righe di parametri. Se un elemento della matrice è impostato su SQL_PARAM_IGNORE, il set di parametri corrispondente a tale elemento viene escluso dalla chiamata a **SQLExecute** o **SQLExecDirect** . La matrice a cui fa riferimento l'attributo SQL_ATTR_PARAM_OPERATION_PTR viene allocata e compilata dall'applicazione e letta dal driver. Se le righe recuperate vengono utilizzate come parametri di input, è possibile utilizzare i valori della matrice di stato della riga nella matrice di operazioni dei parametri.  
  
## <a name="error-processing"></a>Errore di elaborazione  
 Se si verifica un errore durante l'esecuzione dell'istruzione, la funzione di esecuzione restituisce un errore e imposta la variabile del numero di riga sul numero della riga contenente l'errore. Si tratta di un'origine dati specifica se vengono eseguite tutte le righe eccetto il set di errori o se vengono eseguite tutte le righe prima, ma non dopo, il set di errori. Dal momento che elabora i set di parametri, il driver imposta il buffer specificato dall'attributo dell'istruzione SQL_ATTR_PARAMS_PROCESSED_PTR sul numero della riga in fase di elaborazione. Se vengono eseguiti tutti i set eccetto il set di errori, il driver imposta questo buffer su SQL_ATTR_PARAMSET_SIZE dopo l'elaborazione di tutte le righe.  
  
 Se è stato impostato l'attributo dell'istruzione SQL_ATTR_PARAM_STATUS_PTR, **SQLExecute** o **SQLExecDirect** restituisce la *matrice di stato del parametro,* che fornisce lo stato di ogni set di parametri. La matrice di stato del parametro viene allocata dall'applicazione e compilata dal driver. I relativi elementi indicano se l'istruzione SQL è stata eseguita correttamente per la riga di parametri o se si è verificato un errore durante l'elaborazione del set di parametri. Se si è verificato un errore, il driver imposta il valore corrispondente nella matrice di stato del parametro su SQL_PARAM_ERROR e restituisce SQL_SUCCESS_WITH_INFO. L'applicazione può controllare la matrice di stato per determinare quali righe sono state elaborate. Utilizzando il numero di riga, l'applicazione può spesso correggere l'errore e riprendere l'elaborazione.  
  
 Il modo in cui viene utilizzata la matrice di stato dei parametri è determinato dall'SQL_PARAM_ARRAY_ROW_COUNTS e dalle opzioni di SQL_PARAM_ARRAY_SELECTS restituite da una chiamata a **SQLGetInfo**. Per le istruzioni **Insert**, **Update**e **Delete** , la matrice di stato del parametro viene compilata con le informazioni sullo stato se viene restituito SQL_PARC_BATCH per SQL_PARAM_ARRAY_ROW_COUNTS, ma non se SQL_PARC_NO_BATCH viene restituito. Per le istruzioni **Select** , la matrice di stato del parametro viene compilata se SQL_PAS_BATCH viene restituito per SQL_PARAM_ARRAY_SELECT, ma non se viene restituito SQL_PAS_NO_BATCH o SQL_PAS_NO_SELECT.  
  
## <a name="data-at-execution-parameters"></a>Parametri data-at-execution  
 Se uno dei valori nella matrice di lunghezza/indicatore è SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC (*length*), i dati relativi a tali valori vengono inviati con **SQLPutData** nel modo consueto. Gli aspetti seguenti di questo processo portano commenti speciali perché non sono immediatamente evidenti:  
  
-   Quando il driver restituisce SQL_NEED_DATA, deve impostare l'indirizzo della variabile di numero di riga sulla riga per cui sono necessari i dati. Come nel caso a valore singolo, l'applicazione non può ipotizzare l'ordine in cui il driver richiederà i valori dei parametri all'interno di un singolo set di parametri. Se si verifica un errore durante l'esecuzione di un parametro data-at-execution, il buffer specificato dall'attributo dell'istruzione SQL_ATTR_PARAMS_PROCESSED_PTR viene impostato sul numero della riga in cui si è verificato l'errore, lo stato della riga nella matrice di stato della riga specificata dall'attributo SQL_ATTR_PARAM_STATUS_PTR istruzione è impostato su SQL_PARAM_ERROR e la chiamata a **SQLExecute**, **SQLExecDirect**, **SQLParamData**o **SQLPutData** restituisce SQL_ERROR. Il contenuto di questo buffer non è definito se **SQLExecute**, **SQLExecDirect**o **SQLParamData** restituiscono SQL_STILL_EXECUTING.  
  
-   Poiché il driver non interpreta il valore nell'argomento *ParameterValuePtr* di **SQLBindParameter** per i parametri data-at-execution, se l'applicazione fornisce un puntatore a una matrice, **SQLParamData** non estrae e restituisce un elemento di questa matrice all'applicazione. Restituisce invece il valore scalare fornito dall'applicazione. Ciò significa che il valore restituito da **SQLParamData** non è sufficiente per specificare il parametro per il quale l'applicazione deve inviare i dati; l'applicazione deve anche considerare il numero di riga corrente.  
  
     Quando solo alcuni degli elementi di una matrice di parametri sono parametri data-at-execution, l'applicazione deve passare l'indirizzo di una matrice in *ParameterValuePtr* che contiene elementi per tutti i parametri. Questa matrice viene interpretata normalmente per i parametri che non sono parametri data-at-execution. Per i parametri data-at-execution, il valore fornito da **SQLParamData** all'applicazione, che in genere può essere usato per identificare i dati che il driver richiede in questa circostanza, è sempre l'indirizzo della matrice.
