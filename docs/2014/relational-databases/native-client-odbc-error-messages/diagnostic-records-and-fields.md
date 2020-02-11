---
title: Campi e record di diagnostica | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- header records [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], diagnostic records
- ODBC error handling, diagnostic records
- SQLGetDiagField function
- diagnostic records [ODBC]
- errors [ODBC], diagnostic records
- fields [ODBC]
- status information [ODBC]
ms.assetid: 4949530c-62d1-4f1a-b592-144244444ce0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 173d0287ba1b63e8811e2d340448d03c3bbf961d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63213929"
---
# <a name="diagnostic-records-and-fields"></a>Campi e record di diagnostica
  I record di diagnostica sono associati a handle descrittore, di istruzione, di connessione o di ambiente ODBC. Quando una funzione ODBC genera un codice restituito diverso da SQL_SUCCESS o SQL_INVALID_HANDLE, l'handle chiamato dalla funzione presenta record di diagnostica associati che contengono messaggi informativi o di errore. Questi record vengono mantenuti fino a quando non vengono eliminati per effetto di una chiamata a un'altra funzione utilizzando l'handle specifico. Non esiste un limite nel numero di record di diagnostica che possono essere associati a un handle.  
  
 Sono disponibili due tipi di record di diagnostica, ovvero di intestazione e di stato. Il record di intestazione è il record 0, mentre gli eventuali record di stato vengono numerati a partire da 1. I record di diagnostica contengono campi diversi per il record di intestazione e i record di stato. Per i componenti ODBC possono anche essere definiti campi dei record di diagnostica specifici.  
  
 I campi del record di intestazione contengono informazioni generali sull'esecuzione di una funzione, inclusi il codice restituito, il conteggio delle righe, il numero di record di stato e il tipo di istruzione eseguita. Il record di intestazione viene creato sempre, a meno che una funzione ODBC non restituisca SQL_INVALID_HANDLE. Per un elenco completo dei campi nel record di intestazione, vedere [SQLGetDiagField](../native-client-odbc-api/sqlgetdiagfield.md).  
  
 I campi dei record di stato contengono informazioni su errori o avvisi specifici restituiti da Gestione driver ODBC, dal driver o dall'origine dati, quali SQLSTATE, il numero dell'errore nativo, il messaggio di diagnostica, il numero di colonna e il numero di riga. I record di stato vengono creati solo se la funzione restituisce SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA o SQL_STILL_EXECUTING. Per un elenco completo dei campi nei record di stato, vedere **SQLGetDiagField**.  
  
 **SQLGetDiagRec** recupera un singolo record di diagnostica insieme ai campi ODBC SQLSTATE, numero di errore nativo e messaggio di diagnostica. Questa funzionalità è simile a ODBC 2. _x_**SQLError** (funzione). Funzione di gestione degli errori più semplice in ODBC 3. *x* è possibile chiamare ripetutamente **SQLGetDiagRec** a partire dal parametro *RecNumber* impostato su 1 e incrementando *RecNumber* per 1 fino a quando **SQLGetDiagRec** non restituisce SQL_NO_DATA. Equivale a ODBC 2. applicazione *x* che chiama **SQLError** fino a quando non restituisce SQL_NO_DATA_FOUND.  
  
 ODBC 3. *x* supporta molto più informazioni di diagnostica rispetto a ODBC 2. *x*. Queste informazioni vengono archiviate in campi aggiuntivi nei record di diagnostica recuperati tramite **SQLGetDiagField**.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client dispone di campi di diagnostica specifici del driver che possono essere recuperati con **SQLGetDiagField**. Le etichette di questi campi specifici del driver sono definite in sqlncli.h. Utilizzarle per recuperare lo stato, il livello di gravità, il nome del server, il nome della procedura e il numero di riga di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associati a ogni record di diagnostica. Inoltre, sqlncli. h contiene le definizioni dei codici utilizzati dal driver per identificare le istruzioni Transact-SQL se un'applicazione chiama **SQLGetDiagField** con *DiagIdentifier* impostato su SQL_DIAG_DYNAMIC_FUNCTION_CODE.  
  
 **SQLGetDiagField** viene elaborato da Gestione driver ODBC utilizzando le informazioni sugli errori memorizzate nella cache dal driver sottostante. Gestione driver ODBC memorizza nella cache i campi di diagnostica specifici del driver solo una volta stabilita una connessione. **SQLGetDiagField** restituisce SQL_ERROR se viene chiamato per ottenere i campi di diagnostica specifici del driver prima che una connessione venga completata correttamente. Se una funzione di connessione ODBC restituisce SQL_SUCCESS_WITH_INFO, i campi di diagnostica specifici del driver della funzione non sono ancora disponibili. È possibile iniziare a chiamare **SQLGetDiagField** per i campi di diagnostica specifici del driver solo dopo aver eseguito un'altra chiamata di funzione ODBC dopo la funzione Connect.  
  
 La maggior parte degli errori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] segnalati dal driver ODBC di Native client può essere diagnosticata efficacemente utilizzando solo le informazioni restituite da **SQLGetDiagRec**. In alcuni casi, tuttavia, le informazioni restituite dai campi di diagnostica specifici del driver sono importanti per la diagnosi di un errore. Quando si codifica un gestore degli errori ODBC per le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] applicazioni che utilizzano il driver ODBC di Native client, è consigliabile utilizzare anche **SQLGetDiagField** per recuperare almeno i campi SQL_DIAG_SS_MSGSTATE e SQL_DIAG_SS_SEVERITY specifici del driver. Se un determinato errore può essere generato in diverse posizioni nel codice [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL_DIAG_SS_MSGSTATE indica esattamente al supporto tecnico Microsoft il punto in cui è stato generato, fornendo in tal modo un'informazione che in alcuni casi facilita la diagnosi di un problema.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di errori e messaggi](handling-errors-and-messages.md)  
  
  
