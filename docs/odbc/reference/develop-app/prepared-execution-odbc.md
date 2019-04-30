---
title: Preparare l'esecuzione ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c7bd6bc8281dd6bdc3bcfbd437380b2d5269ee43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199109"
---
# <a name="prepared-execution-odbc"></a>Esecuzione preparata ODBC
Esecuzione preparata è un modo efficiente per eseguire un'istruzione più volte. L'istruzione viene compilata prima di tutto, oppure *preparata,* in un piano di accesso. Il piano di accesso viene quindi eseguita una o più volte in un secondo momento. Per altre informazioni sui piani di accesso, vedere [elaborazione di un'istruzione SQL](../../../odbc/reference/processing-a-sql-statement.md).  
  
 Esecuzione preparata viene comunemente utilizzata dalle applicazioni personalizzate e verticale per eseguire ripetutamente la stessa istruzione SQL con parametri. Ad esempio, il codice seguente prepara un'istruzione per aggiornare i prezzi delle varie parti. Ed esegue l'istruzione più volte con valori di parametro diversi ogni volta.  
  
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
  
 Esecuzione preparata è più veloce di esecuzione diretta per le istruzioni eseguite più volte, principalmente perché l'istruzione viene compilata solo una volta. le istruzioni eseguite direttamente vengono compilate ogni volta che vengono eseguite. Esecuzione preparata anche possibile fornire che una riduzione del traffico di rete perché il driver può inviare un identificatore del piano di accesso all'origine dati ogni volta che l'istruzione viene eseguita, anziché un'intera istruzione SQL, se l'origine dati supporta l'accesso identificatori dei piani.  
  
 L'applicazione può recuperare i metadati per il gruppo di risultati dopo l'istruzione viene preparata e prima che venga eseguito. Tuttavia, restituzione dei metadati per la preparazione, è dispendiosa per alcuni driver e dovrebbe essere evitata da applicazioni interoperative, se possibile istruzioni non eseguite. Per altre informazioni, vedere [metadati dei Set di risultati](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 L'esecuzione preparata non deve essere utilizzata per le istruzioni eseguite una sola volta. Per tali istruzioni è leggermente più lento rispetto esecuzione diretta perché richiede una chiamata di funzione ODBC aggiuntiva.  
  
> [!IMPORTANT]  
>  Eseguire il commit o rollback di una transazione, in modo esplicito chiamando **SQLEndTran** o la possibilità di lavorare in modalità autocommit, fa sì che alcune origini dati eliminare i piani di accesso per tutte le istruzioni in una connessione. Per altre informazioni, vedere le opzioni SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR nel [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrizione della funzione.  
  
 Preparare ed eseguire un'istruzione, l'applicazione:  
  
1.  Le chiamate **SQLPrepare** e lo passa a una stringa contenente l'istruzione SQL.  
  
2.  Imposta i valori dei parametri. Parametri possono essere impostati in realtà prima o dopo la preparazione dell'istruzione. Per altre informazioni, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.  
  
3.  Le chiamate **SQLExecute** ed effettua elaborazioni aggiuntive che è necessario, ad esempio il recupero dei dati.  
  
4.  Ripetere i passaggi da 2 e 3 in base alle esigenze.  
  
5.  Quando **SQLPrepare** viene chiamato, il driver:  
  
    -   Consente di modificare l'istruzione SQL per usare la grammatica SQL dell'origine dati senza analizzare l'istruzione. Sono inclusi sostituendo le sequenze di escape descritte in [sequenze di Escape in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). L'applicazione può recuperare il modulo di un'istruzione SQL modificato chiamando **SQLNativeSql**. Se è impostato l'attributo di istruzione SQL_ATTR_NOSCAN, le sequenze di escape non vengono sostituite.  
  
    -   Invia l'istruzione all'origine dati per la preparazione.  
  
    -   Archivia l'identificatore del piano di accesso restituito per un'esecuzione successiva (se l'elaborazione ha avuto esito positivo) o restituisce eventuali errori (se la preparazione non riuscita). Gli errori sono errori sintattici, ad esempio SQLSTATE 42000 (sintassi o violazione di accesso) e semantici, ad esempio 42S02 SQLSTATE (di Base nella tabella o vista non trovato).  
  
        > [!NOTE]  
        >  Alcuni driver non restituire gli errori a questo punto ma invece li quando viene eseguita l'istruzione o quando vengono chiamate le funzioni di catalogo. Pertanto **SQLPrepare** potrebbe sembrare che hanno avuto esito positivo quando in realtà non è riuscito.  
  
6.  Quando **SQLExecute** viene chiamato, il driver:  
  
    -   Recupera i valori di parametro corrente e li converte in base alle esigenze. Per altre informazioni, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.  
  
    -   Invia l'identificatore del piano di accesso e i valori di parametro convertito nell'origine dati.  
  
    -   Restituisce gli eventuali errori. Si tratta di errori a livello generale in fase di esecuzione, ad esempio SQLSTATE 24000 (stato del cursore non valido). Tuttavia, alcuni driver restituire errori sintattici e semantici a questo punto.  
  
 Se l'origine dati non supporta preparazione dell'istruzione, il driver deve emulare si misura. Ad esempio, il driver potrà non fare nulla quando **SQLPrepare** viene chiamato e quindi eseguire l'esecuzione diretta dell'istruzione quando **SQLExecute** viene chiamato.  
  
 Se l'origine dati supporta il controllo senza l'esecuzione della sintassi, il driver può inviare l'istruzione per il controllo quando **SQLPrepare** viene chiamato e inviare l'istruzione per l'esecuzione quando **SQLExecute** è viene chiamato.  
  
 Se il driver non è possibile emulare una preparazione dell'istruzione, archivia l'istruzione quando **SQLPrepare** viene chiamato e inviata per l'esecuzione quando **SQLExecute** viene chiamato.  
  
 Perché non è perfetta, preparazione dell'istruzione emulato **SQLExecute** può restituire eventuali errori restituiti normalmente da **SQLPrepare**.
