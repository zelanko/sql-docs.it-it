---
title: Funzioni API di livello 2 (driver ODBC per Oracle) | Microsoft Docs
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
ms.openlocfilehash: 7600734fef44071b1f5e35c136a6b9facdb8b390
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949033"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>Funzioni API di livello 2 (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Le funzioni a questo livello forniscono una conformità dell'interfaccia di livello 1, oltre a funzionalità aggiuntive quali il supporto per segnalibri, parametri dinamici e l'esecuzione asincrona di funzioni ODBC.  
  
|Funzione API|Note|  
|------------------|-----------|  
|**SQLBindParameter**|Associa un buffer a un marcatore di parametro in un'istruzione SQL.|  
|**SQLBrowseConnect**|Restituisce i livelli successivi di attributi e valori di attributo.|  
|**SQLDataSources**|Elenca i nomi delle origini dati. Implementato da Gestione driver.|  
|**SQLDescribeParam**|Restituisce la descrizione di un marcatore di parametro associato a un'istruzione SQL preparata.<br /><br /> Restituisce una migliore stima dell'elemento del parametro, in base all'analisi dell'istruzione. Se non è possibile determinare il tipo di parametro, SQL_VARCHAR restituisce un risultato di lunghezza 2000.|  
|**SQLDrivers**|Implementato da Gestione driver.|  
|**SQLExtendedFetch**|Simile a **SQLFetch** ma restituisce più righe usando una matrice per ogni colonna. Il set di risultati è scorrevole per lo scorrimento avanti e può essere reso di scorrimento a ritroso se il cursore è definito come statico, non solo in avanti. Per i cursori di sola lettura con associazione di colonna predefinita, i dati di colonna dei set di dati di dimensioni maggiori rispetto all'attributo di connessione BUFFERSIZE vengono recuperati direttamente nei buffer di dati. Non supporta i segnalibri a lunghezza variabile e non supporta il recupero di un set di righe con un offset (diverso da 0) da un segnalibro.|  
|**SQLForeignKeys**|Restituisce un elenco di chiavi esterne in una singola tabella o un elenco di chiavi esterne in altre tabelle che fanno riferimento a una singola tabella.|  
|**SQLMoreResults**|Determina se più risultati sono in sospeso in un handle di istruzione, hstmt, che contiene istruzioni SELECT, UPDATE, INSERT o DELETE e, in caso affermativo, Inizializza l'elaborazione per tali risultati.<br /><br /> Oracle supporta più set di risultati solo da stored procedure, quando si utilizzano sequenze di escape {ResultSet...}.|  
|**SQLNativeSql**|Per informazioni sull'utilizzo, vedere [restituzione di parametri di matrice da stored procedure](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLNumParams**|Restituisce il numero di parametri in un'istruzione SQL. Il numero di parametri deve essere uguale al numero di punti interrogativi nell'istruzione SQL passata a **SQLPrepare**.|  
|**SQLPrimaryKeys**|Restituisce i nomi delle colonne che costituiscono la chiave primaria per una tabella.|  
|**SQLProcedureColumns**|Restituisce un elenco di parametri di input e di output, il valore restituito, le colonne nel set di risultati di una singola procedura e due colonne aggiuntive, OVERLOAD e ORDINAL_POSITION. OVERLOAD è la colonna di OVERLOAD della tabella ALL_ARGUMENTS della visualizzazione del dizionario dei dati Oracle. ORDINAL_POSITION è la colonna sequenza della tabella ALL_ARGUMENTS della visualizzazione del dizionario dei dati Oracle. Per le procedure in pacchetto, la colonna nome procedura si trova nel formato *PackageName. ProcedureName* . Non restituisce le colonne procedure di un sinonimo creato che fa riferimento a una procedura o a una funzione.|  
|**SQLProcedures**|Restituisce un elenco di procedure nell'origine dati. Per le procedure in pacchetto, la colonna nome procedura si trova nel formato *PackageName. ProcedureName* .<br /><br /> Poiché Oracle non fornisce un modo per distinguere le procedure in pacchetto dalle funzioni incluse nel pacchetto, il driver restituisce SQL_PT_UNKNOWN per la colonna PROCEDURE_TYPE.|  
|**SQLSetPos**|Imposta la posizione del cursore in un set di righe. È possibile utilizzare **SQLSetPos** con **SQLGetData** per recuperare righe dalle colonne non associate dopo aver posizionato il cursore su una riga specifica del set di righe. Le righe aggiunte al set di risultati utilizzando *fOption* SQL_ADD vengono aggiunte dopo l'ultima riga nel set di risultati.|  
|**SQLSetScrollOptions**|Imposta le opzioni che controllano il comportamento dei cursori associati a un handle di istruzione, hstmt. Per informazioni dettagliate, vedere [tipi di cursore e combinazioni di concorrenza](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|
