---
description: Esecuzione preparata ODBC
title: ODBC di esecuzione preparata | Microsoft Docs
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
ms.openlocfilehash: 6141af2cde7106419ab1eb68f86d5817f055aab2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465743"
---
# <a name="prepared-execution-odbc"></a>Esecuzione preparata ODBC
L'esecuzione preparata è un modo efficiente per eseguire un'istruzione più di una volta. L'istruzione viene prima compilata o *preparata* in un piano di accesso. Il piano di accesso viene quindi eseguito una o più volte in un secondo momento. Per ulteriori informazioni sui piani di accesso, vedere [elaborazione di un'istruzione SQL](../../../odbc/reference/processing-a-sql-statement.md).  
  
 L'esecuzione preparata viene comunemente utilizzata dalle applicazioni verticali e personalizzate per eseguire ripetutamente la stessa istruzione SQL con parametri. Il codice seguente, ad esempio, prepara un'istruzione per l'aggiornamento dei prezzi delle diverse parti. Esegue quindi l'istruzione più volte con valori di parametro diversi ogni volta.  
  
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
  
 L'esecuzione preparata è più veloce dell'esecuzione diretta per le istruzioni eseguite più volte, principalmente perché l'istruzione viene compilata una sola volta. le istruzioni eseguite direttamente vengono compilate ogni volta che vengono eseguite. L'esecuzione preparata può anche fornire una riduzione del traffico di rete perché il driver può inviare un identificatore del piano di accesso all'origine dati ogni volta che viene eseguita l'istruzione, anziché un'intera istruzione SQL, se l'origine dati supporta gli identificatori del piano di accesso.  
  
 L'applicazione può recuperare i metadati per il set di risultati dopo che l'istruzione è stata preparata e prima di essere eseguita. Tuttavia, la restituzione di metadati per istruzioni preparate e non eseguite è dispendiosa per alcuni driver e deve essere evitata dalle applicazioni interoperative, se possibile. Per ulteriori informazioni, vedere [metadati del set di risultati](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 L'esecuzione preparata non deve essere utilizzata per le istruzioni eseguite una sola volta. Per tali istruzioni, è leggermente più lento rispetto all'esecuzione diretta, perché richiede una chiamata di funzione ODBC aggiuntiva.  
  
> [!IMPORTANT]  
>  Per eseguire il commit o il rollback di una transazione, chiamando in modo esplicito **SQLEndTran** o utilizzando la modalità autocommit, alcune origini dati possono eliminare i piani di accesso per tutte le istruzioni in una connessione. Per ulteriori informazioni, vedere le opzioni SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR nella descrizione della funzione [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .  
  
 Per preparare ed eseguire un'istruzione, l'applicazione:  
  
1.  Chiama **SQLPrepare** e lo passa a una stringa contenente l'istruzione SQL.  
  
2.  Imposta i valori di tutti i parametri. I parametri possono essere effettivamente impostati prima o dopo la preparazione dell'istruzione. Per ulteriori informazioni, vedere [parametri di istruzione](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.  
  
3.  Chiama **SQLExecute** ed esegue altre operazioni di elaborazione necessarie, ad esempio il recupero dei dati.  
  
4.  Se necessario, ripete i passaggi 2 e 3.  
  
5.  Quando viene chiamato **SQLPrepare** , il driver:  
  
    -   Modifica l'istruzione SQL in modo che utilizzi la grammatica SQL dell'origine dati senza analizzare l'istruzione. Ciò include la sostituzione delle sequenze di escape descritte in [sequenze di escape in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). L'applicazione può recuperare il formato modificato di un'istruzione SQL chiamando **SQLNativeSql**. Le sequenze di escape non vengono sostituite se è impostato l'attributo dell'istruzione SQL_ATTR_NOSCAN.  
  
    -   Invia l'istruzione all'origine dati per la preparazione.  
  
    -   Archivia l'identificatore del piano di accesso restituito per l'esecuzione successiva (se la preparazione ha avuto esito positivo) o restituisce eventuali errori (se la preparazione ha avuto esito negativo). Gli errori includono errori sintattici come SQLSTATE 42000 (errore di sintassi o violazione di accesso) ed errori semantici come SQLSTATE 42S02 (tabella di base o vista non trovata).  
  
        > [!NOTE]  
        >  Alcuni driver non restituiscono errori in questa fase, ma li restituiscono quando viene eseguita l'istruzione o quando vengono chiamate le funzioni di catalogo. Di conseguenza, **SQLPrepare** potrebbe sembrare che abbia avuto esito positivo quando in realtà ha avuto esito negativo.  
  
6.  Quando viene chiamato **SQLExecute** , il driver:  
  
    -   Recupera i valori di parametro correnti e li converte secondo necessità. Per ulteriori informazioni, vedere [parametri di istruzione](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.  
  
    -   Invia l'identificatore del piano di accesso e i valori dei parametri convertiti nell'origine dati.  
  
    -   Restituisce eventuali errori. Si tratta in genere di errori in fase di esecuzione, ad esempio SQLSTATE 24000 (stato del cursore non valido). A questo punto, tuttavia, alcuni driver restituiscono errori sintattici e semantici.  
  
 Se l'origine dati non supporta la preparazione delle istruzioni, il driver deve emularlo nella misura massima consentita. Ad esempio, il driver potrebbe non eseguire alcuna operazione quando viene chiamato **SQLPrepare** , quindi eseguire l'esecuzione diretta dell'istruzione quando viene chiamato **SQLExecute** .  
  
 Se l'origine dati supporta il controllo della sintassi senza esecuzione, il driver potrebbe inviare l'istruzione per verificare quando viene chiamato **SQLPrepare** e inviare l'istruzione per l'esecuzione quando viene chiamato **SQLExecute** .  
  
 Se il driver non è in grado di emulare la preparazione delle istruzioni, archivia l'istruzione quando viene chiamato **SQLPrepare** e lo invia per l'esecuzione quando viene chiamato **SQLExecute** .  
  
 Poiché la preparazione dell'istruzione emulata non è perfetta, **SQLExecute** può restituire tutti gli errori normalmente restituiti da **SQLPrepare**.
