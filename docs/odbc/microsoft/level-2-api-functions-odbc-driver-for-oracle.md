---
title: Funzioni API di livello 2 (Driver ODBC per Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be472a4a99324927128514fa9f8cbf19d44d49cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63262253"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>Funzioni API di livello 2 (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Funzioni a questo livello forniscono conformità di interfaccia di livello 1 oltre a funzionalità aggiuntive, ad esempio il supporto per i segnalibri, i parametri dinamici e l'esecuzione asincrona delle funzioni ODBC.  
  
|Funzione dell'API|Note|  
|------------------|-----------|  
|**SQLBindParameter**|Associa un buffer con un marcatore di parametro in un'istruzione SQL.|  
|**SQLBrowseConnect**|Restituisce i livelli successivi degli attributi e valori di attributo.|  
|**SQLDataSources**|Elenca i nomi delle origini dati. Implementata da Gestione Driver.|  
|**SQLDescribeParam**|Restituisce la descrizione di un marcatore di parametro associato a un'istruzione SQL preparata.<br /><br /> Restituisce una stima del quale il parametro è, in base all'analisi dell'istruzione. Se non è possibile determinare il tipo di parametro, lunghezza 2000 restituisce SQL_VARCHAR.|  
|**SQLDrivers**|Implementata da Gestione Driver.|  
|**SQLExtendedFetch**|Simile a **SQLFetch** ma restituisce più righe utilizzando una matrice per ogni colonna. Il set di risultati forward-supporta lo scorrimento e può essere eseguito con le versioni precedenti-scorrevole se il cursore viene definito come static e non forward-only. Per i cursori forward-only con associazione di colonna predefinita, vengono recuperati i dati della colonna dal set di dati più grande rispetto all'attributo di connessione BUFFERSIZE direttamente nel buffer di dati. Non supporta i segnalibri di lunghezza variabile e non supporta il recupero di un set di righe in un offset (diverso da 0) da un segnalibro.|  
|**SQLForeignKeys**|Restituisce un elenco di chiavi esterne in una singola tabella o un elenco di chiavi esterne in altre tabelle che fanno riferimento a una singola tabella.|  
|**SQLMoreResults**|Determina se i risultati di ulteriori sono in sospeso su un handle di istruzione, hstmt, che contiene istruzioni SELECT, UPDATE, INSERT o DELETE e in questo caso, inizializza l'elaborazione per i risultati ottenuti.<br /><br /> Oracle supporta più i set di risultati solo dalle stored procedure, quando si usa sequenze di escape {resultset}.|  
|**SQLNativeSql**|Per informazioni sull'utilizzo, vedere [restituzione di parametri di matrice dalle Stored procedure](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLNumParams**|Restituisce il numero di parametri in un'istruzione SQL. Il numero di parametri deve uguale al numero di punti interrogativi nell'istruzione SQL passata al **SQLPrepare**.|  
|**SQLPrimaryKeys**|Restituisce i nomi delle colonne che costituiscono la chiave primaria per una tabella.|  
|**SQLProcedureColumns**|Restituisce un elenco di parametri di input e output, il valore restituito, le colonne in set di risultati di una sola stored procedure e due colonne aggiuntive, OVERLOAD e ORDINAL_POSITION. OVERLOAD è la colonna OVERLOAD dalla tabella ALL_ARGUMENTS della vista di dizionario di dati Oracle. ORDINAL_POSITION è la colonna di sequenza della tabella ALL_ARGUMENTS della vista di dizionario di dati Oracle. Per le procedure in pacchetto, nella colonna nome della procedura si *packagename.procedurename* formato. Non restituisce le colonne di procedure di un sinonimo creato che fa riferimento a una procedura o funzione.|  
|**SQLProcedures**|Restituisce un elenco di procedure nell'origine dati. Per le procedure in pacchetto, nella colonna nome della procedura si *packagename.procedurename* formato.<br /><br /> Poiché non fornisce un modo per distinguere le procedure in pacchetto da funzioni di package Oracle, il driver restituisce SQL_PT_UNKNOWN per la colonna PROCEDURE_TYPE.|  
|**SQLSetPos**|Imposta la posizione del cursore in un set di righe. È possibile usare **SQLSetPos** con **SQLGetData** per recuperare righe da colonne non associate dopo posizionando il cursore in una riga specifica nel set di righe. Righe aggiunte per il set di risultati utilizzando *fOption* SQL_ADD vengono aggiunti dopo l'ultima riga nel set di risultati.|  
|**SQLSetScrollOptions**|Imposta le opzioni che controllano il comportamento dei cursori associata a un handle di istruzione, hstmt. Per informazioni dettagliate, vedere [tipo di cursore e concorrenza combinazioni](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|
