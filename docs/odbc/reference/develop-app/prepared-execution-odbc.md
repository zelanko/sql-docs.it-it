---
title: ODBC di esecuzione preparata . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 147ca85b21296575ff55afbe66ab286cc4824fae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282311"
---
# <a name="prepared-execution-odbc"></a>Esecuzione preparata ODBC
L'esecuzione preparata è un modo efficiente per eseguire un'istruzione più di una volta. L'istruzione viene prima compilata, o *preparata,* in un piano di accesso. Il piano di accesso viene quindi eseguito una o più volte in un secondo momento. Per ulteriori informazioni sui piani di accesso, vedere [Elaborazione di un'istruzione SQL](../../../odbc/reference/processing-a-sql-statement.md).  
  
 L'esecuzione preparata viene comunemente utilizzata dalle applicazioni verticali e personalizzate per eseguire ripetutamente la stessa istruzione SQL con parametri. Ad esempio, il codice seguente prepara un'istruzione per aggiornare i prezzi delle diverse parti. L'istruzione viene quindi eseguita più volte con valori di parametro diversi ogni volta.  
  
```  
SQLREAL       Price;  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0, PriceInd = 0;  
  
// Prepare a statement to update salaries in the Employees table.  
SQLPrepare(hstmt, "UPDATE Parts SET Price = ? WHERE PartID = ?", SQL_NTS);  
  
// Bind Price to the parameter for the Price column and PartID to  
// the parameter for the PartID column.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &PartID, 0, &PartIDInd);  
  
// Repeatedly execute the statement.  
while (GetPrice(&PartID, &Price)) {  
   SQLExecute(hstmt);  
}  
```  
  
 L'esecuzione preparata è più veloce dell'esecuzione diretta per le istruzioni eseguite più di una volta, principalmente perché l'istruzione viene compilata una sola volta; le istruzioni eseguite direttamente vengono compilate ogni volta che vengono eseguite. L'esecuzione preparata può anche fornire una riduzione del traffico di rete perché il driver può inviare un identificatore del piano di accesso all'origine dati ogni volta che viene eseguita l'istruzione, anziché un'intera istruzione SQL, se l'origine dati supporta gli identificatori del piano di accesso.  
  
 L'applicazione può recuperare i metadati per il set di risultati dopo la preparazione dell'istruzione e prima che venga eseguita. Tuttavia, la restituzione di metadati per istruzioni preparate e non eseguite è costosa per alcuni driver e deve essere evitata dalle applicazioni interoperabili, se possibile. Per ulteriori informazioni, consultate [Metadati del set di risultati](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 L'esecuzione preparata non deve essere utilizzata per le istruzioni eseguite una sola volta. Per tali istruzioni, è leggermente più lento rispetto all'esecuzione diretta perché richiede una chiamata di funzione ODBC aggiuntiva.  
  
> [!IMPORTANT]  
>  Il commit o il rollback di una transazione, chiamando in modo esplicito **SQLEndTran** o utilizzando la modalità di commit automatico, fa sì che alcune origini dati eliminino i piani di accesso per tutte le istruzioni in una connessione. Per altre informazioni, vedere le opzioni SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR nella descrizione della funzione [SQLGetInfo.For](../../../odbc/reference/syntax/sqlgetinfo-function.md) more information, see the SQL_CURSOR_COMMIT_BEHAVIOR and SQL_CURSOR_ROLLBACK_BEHAVIOR options in the SQLGetInfo function description.  
  
 Per preparare ed eseguire un'istruzione, l'applicazione:  
  
1.  Chiama **SQLPrepare** e passa una stringa contenente l'istruzione SQL.  
  
2.  Imposta i valori di tutti i parametri. I parametri possono essere impostati prima o dopo la preparazione dell'istruzione. Per ulteriori informazioni, vedere [Parametri dell'istruzione](../../../odbc/reference/develop-app/statement-parameters.md)più avanti in questa sezione.  
  
3.  Chiama **SQLExecute** ed esegue qualsiasi elaborazione aggiuntiva necessaria, ad esempio il recupero dei dati.  
  
4.  Ripetere i passaggi 2 e 3 in base alle esigenze.  
  
5.  Quando SQLPrepare viene chiamato, il driver:When **SQLPrepare** is called, the driver:  
  
    -   Modifica l'istruzione SQL per utilizzare la grammatica SQL dell'origine dati senza analizzare l'istruzione. Ciò include la sostituzione delle sequenze di escape descritte in Sequenze di [escape in ODBC.](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) L'applicazione può recuperare il formato modificato di un'istruzione SQL chiamando **SQLNativeSql**. Le sequenze di escape non vengono sostituite se è impostato l'attributo dell'istruzione SQL_ATTR_NOSCAN.  
  
    -   Invia l'istruzione all'origine dati per la preparazione.  
  
    -   Archivia l'identificatore del piano di accesso restituito per l'esecuzione successiva (se la preparazione ha avuto esito positivo) o restituisce eventuali errori (se la preparazione non è riuscita). Gli errori includono errori sintattici come SQLSTATE 42000 (errore di sintassi o violazione di accesso) ed errori semantici come SQLSTATE 42S02 (tabella di base o vista non trovata).  
  
        > [!NOTE]  
        >  Alcuni driver non restituiscono errori a questo punto, ma li restituiscono quando viene eseguita l'istruzione o quando vengono chiamate le funzioni di catalogo. Pertanto, **SQLPrepare** potrebbe sembrare avere esito positivo quando in realtà non è riuscito.  
  
6.  Quando **SQLExecute** viene chiamato, il driver:  
  
    -   Recupera i valori dei parametri correnti e li converte in base alle esigenze. Per ulteriori informazioni, vedere [Parametri dell'istruzione](../../../odbc/reference/develop-app/statement-parameters.md)più avanti in questa sezione.  
  
    -   Invia l'identificatore del piano di accesso e i valori dei parametri convertiti all'origine dati.  
  
    -   Restituisce eventuali errori. Si tratta in genere di errori di runtime, ad esempio SQLSTATE 24000 (stato del cursore non valido). Tuttavia, alcuni driver restituiscono errori sintattici e semantici a questo punto.  
  
 Se l'origine dati non supporta la preparazione dell'istruzione, il driver deve emularla nella misura possibile. Ad esempio, il driver potrebbe non eseguire alcuna operazione quando **SQLPrepare** viene chiamato e quindi eseguire l'esecuzione diretta dell'istruzione quando **SQLExecute** viene chiamato.  
  
 Se l'origine dati supporta il controllo della sintassi senza esecuzione, il driver potrebbe inviare l'istruzione per il controllo quando **SQLPrepare** viene chiamato e inviare l'istruzione per l'esecuzione quando **SQLExecute** viene chiamato.  
  
 Se il driver non è in grado di emulare la preparazione dell'istruzione, archivia l'istruzione quando **SQLPrepare** viene chiamato e la invia per l'esecuzione quando **SQLExecute** viene chiamato.  
  
 Poiché la preparazione emulata delle istruzioni non è perfetta, **SQLExecute** può restituire eventuali errori normalmente restituiti da **SQLPrepare**.
