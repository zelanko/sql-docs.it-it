---
title: Conformità dell'interfaccia di livello 2 Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ee57d716cbb93f855e1fd78d41bff62a681eb6c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306163"
---
# <a name="level-2-interface-conformance"></a>Conformità di interfaccia di livello 2
Il livello di conformità dell'interfaccia di livello 2 include la funzionalità a livello di conformità dell'interfaccia di livello 1 più le seguenti caratteristiche:  
  
|||  
|-|-|  
|201|Utilizzare nomi in tre parti di tabelle e viste di database. Per ulteriori informazioni, vedere la funzionalità di supporto della denominazione in due parti 101 in [Conformità dell'interfaccia](../../../odbc/reference/develop-app/level-1-interface-conformance.md)di livello 1.|  
|202|Descrivere i parametri dinamici, chiamando **SQLDescribeDynamic parameters**, by calling SQLDescribeParam .|  
|203|Usare non solo i parametri di input, ma anche i parametri di output e di input/output e i valori dei risultati delle stored procedure.|  
|204|Utilizzare i segnalibri, incluso il recupero dei segnalibri, chiamando **SQLDescribeCol** e **SQLColAttribute** sul numero di colonna 0; recupero in base a un segnalibro, chiamando **SQLFetchScroll** con il *FetchOrientation* argomento impostato su SQL_FETCH_BOOKMARK; e aggiornare, eliminare e recuperare tramite operazioni di segnalibro, chiamando **SQLBulkOperations** con il *Operation* argomento impostato su SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK o SQL_FETCH_BY_BOOKMARK.|  
|205|Recuperare informazioni avanzate sul dizionario dati chiamando **SQLColumnPrivileges**, **SQLForeignKeys**e **SQLTablePrivileges**.|  
|206|Utilizzare le funzioni ODBC anziché le istruzioni SQL per eseguire operazioni di database aggiuntive, chiamando **SQLBulkOperations** con SQL_ADD o **SQLSetPos** con SQL_DELETE o SQL_UPDATE. (Supporto per le chiamate a **SQLSetPos** con il *LockType* argomento impostato su SQL_LOCK_EXCLUSIVE o SQL_LOCK_UNLOCK non fa parte dei livelli di conformità, ma è una funzionalità facoltativa.)|  
|207|Abilitare l'esecuzione asincrona delle funzioni ODBC per le singole istruzioni specificate.|  
|208|Ottenere la SQL_ROWVER colonna di identificazione delle righe delle tabelle, chiamando **SQLSpecialColumns**. (Per ulteriori informazioni, vedere il supporto per **SQLSpecialColumns** con il *IdentifierType* argomento impostato su SQL_BEST_ROWID come funzionalità 20 nella [conformità dell'interfaccia di base](../../../odbc/reference/develop-app/core-interface-conformance.md).|  
|209|Impostare l'attributo dell'istruzione SQL_ATTR_CONCURRENCY su almeno un valore diverso da SQL_CONCUR_READ_ONLY.|  
|210|La possibilità di timeout richiesta di accesso e query SQL (SQL_ATTR_LOGIN_TIMEOUT e SQL_ATTR_QUERY_TIMEOUT).|  
|211|La possibilità di modificare il livello di isolamento predefinito; la possibilità di eseguire transazioni con il livello di isolamento "serializzabile".|
