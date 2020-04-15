---
title: Funzioni API di livello 2 (driver ODBC per Oracle) . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1e181c5863d6b906eaf9a3ba499728c595f0449
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284181"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>Funzioni API di livello 2 (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Le funzioni a questo livello forniscono la conformità dell'interfaccia di livello 1 e funzionalità aggiuntive, ad esempio il supporto per i segnalibri, i parametri dinamici e l'esecuzione asincrona delle funzioni ODBC.  
  
|Funzione API|Note|  
|------------------|-----------|  
|**SQLBindParameter**|Associa un buffer a un marcatore di parametro in un'istruzione SQL.|  
|**SQLBrowseConnect**|Restituisce livelli successivi di attributi e valori di attributo.|  
|**SqlDataSourcesSQLDataSources**|Elenca i nomi delle origini dati. Implementato da Gestione Driver.|  
|**SQLDescribeParam**|Restituisce la descrizione di un marcatore di parametro associato a un'istruzione SQL preparata.<br /><br /> Restituisce un'ipotesi ottimale del parametro, in base all'analisi dell'istruzione. Se non è possibile determinare il tipo di parametro, SQL_VARCHAR restituisce lunghezza 2000.|  
|**SQLDrivers**|Implementato da Gestione Driver.|  
|**Sqlextendedfetch**|Simile a **SQLFetch** ma restituisce più righe utilizzando una matrice per ogni colonna. Il set di risultati è scorrevole in avanti e può essere reso scorrevole all'indietro se il cursore è definito come statico, non forward-only. Per i cursori forward-only con associazione di colonne predefinita, i dati delle colonne dei set di dati più grandi dell'attributo di connessione BUFFERSI-E vengono recuperati direttamente nei buffer di dati. Non supporta i segnalibri di lunghezza variabile e non supporta il recupero di un set di righe in corrispondenza di un offset (diverso da 0) da un segnalibro.|  
|**SQLForeignKeys**|Restituisce un elenco di chiavi esterne in una singola tabella o un elenco di chiavi esterne in altre tabelle che fanno riferimento a una singola tabella.|  
|**SQLMoreResults**|Determina se sono in sospeso più risultati su un handle di istruzione, hstmt, contenente istruzioni SELECT, UPDATE, INSERT o DELETE e, in caso affermativo, inizializza l'elaborazione per tali risultati.<br /><br /> Oracle supporta più set di risultati solo da stored procedure, quando si utilizzano sequenze di escape di tipo ... data e resultset.|  
|**SQLNativeSql**|Per informazioni sull'utilizzo, vedere [Restituzione di parametri di matrice da stored procedure](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLNumParams**|Restituisce il numero di parametri in un'istruzione SQL. Il numero di parametri deve essere uguale al numero di punti interrogativi nell'istruzione SQL passata a **SQLPrepare**.|  
|**SQLPrimaryKeys**|Restituisce i nomi di colonna che costituiscono la chiave primaria di una tabella.|  
|**SQLProcedureColumns**|Restituisce un elenco di parametri di input e output, il valore restituito, le colonne nel set di risultati di una singola procedura e due colonne aggiuntive, OVERLOAD e ORDINAL_POSITION. OVERLOAD è la colonna OVERLOAD della tabella ALL_ARGUMENTS di Oracle Data Dictionary View. ORDINAL_POSITION è la colonna SEQUENCE della tabella ALL_ARGUMENTS della visualizzazione Del dizionario dei dati Oracle. Per le procedure in pacchetto, la colonna NOME PROCEDURE è in formato *nomepacchetto.nomeprocedura.* Non restituisce le colonne di routine di un sinonimo creato che fa riferimento a una routine o a una funzione.|  
|**SQLProcedures**|Restituisce un elenco di procedure nell'origine dati. Per le procedure in pacchetto, la colonna NOME PROCEDURE è in formato *nomepacchetto.nomeprocedura.*<br /><br /> Poiché Oracle non fornisce un modo per distinguere le procedure in pacchetto dalle funzioni in pacchetto, il driver restituisce SQL_PT_UNKNOWN per la colonna PROCEDURE_TYPE.|  
|**SQLSetPos**|Imposta la posizione del cursore in un set di righe. È possibile utilizzare **SQLSetPos** con **SQLGetData** per recuperare le righe dalle colonne non associate dopo aver posizionato il cursore su una riga specifica nel set di righe. Le righe aggiunte al set di risultati *tramite fOption* SQL_ADD vengono aggiunte dopo l'ultima riga nel set di risultati.|  
|**Opzioni SQLSetScrollOptions**|Imposta le opzioni che controllano il comportamento dei cursori associati a un handle di istruzione, hstmt. Per informazioni dettagliate, vedere Combinazioni di tipo [di cursore e concorrenza](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|
