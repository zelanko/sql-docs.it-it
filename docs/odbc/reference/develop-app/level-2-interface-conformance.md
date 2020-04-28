---
title: Conformità di interfaccia di livello 2 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306163"
---
# <a name="level-2-interface-conformance"></a>Conformità di interfaccia di livello 2
Il livello di conformità dell'interfaccia di livello 2 include le funzionalità a livello di conformità dell'interfaccia di livello 1 più le funzionalità seguenti:  
  
|||  
|-|-|  
|201|Utilizzare nomi in tre parti delle tabelle e delle viste di database. Per ulteriori informazioni, vedere la funzionalità di supporto per la denominazione in due parti 101 nella [conformità dell'interfaccia di livello 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md).|  
|202|Descrivere i parametri dinamici chiamando **SQLDescribeParam**.|  
|203|Utilizzare non solo parametri di input, ma anche output e parametri di input/output e i valori dei risultati delle stored procedure.|  
|204|Usare i segnalibri, incluso il recupero dei segnalibri, chiamando **SQLDescribeCol** e **SQLColAttribute** sul numero di colonna 0; recupero basato su un segnalibro, chiamando **SQLFetchScroll** con l'argomento *FetchOrientation* impostato su SQL_FETCH_BOOKMARK; e le operazioni di aggiornamento, eliminazione e recupero tramite segnalibro, chiamando **SQLBulkOperations** con l'argomento *Operation* impostato su SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK o SQL_FETCH_BY_BOOKMARK.|  
|205|Recuperare informazioni avanzate sul dizionario dei dati, chiamando **SQLColumnPrivileges**, **SQLForeignKeys**e **SQLTablePrivileges**.|  
|206|Utilizzare le funzioni ODBC anziché le istruzioni SQL per eseguire operazioni di database aggiuntive, chiamando **SQLBulkOperations** con SQL_ADD o **SQLSetPos** con SQL_DELETE o SQL_UPDATE. Il supporto per le chiamate a **SQLSetPos** con l'argomento *LockType* impostato su SQL_LOCK_EXCLUSIVE o SQL_LOCK_UNLOCK non fa parte dei livelli di conformità ma è una funzionalità facoltativa.|  
|207|Consente l'esecuzione asincrona delle funzioni ODBC per le singole istruzioni specificate.|  
|208|Ottenere la colonna di identificazione SQL_ROWVER riga delle tabelle chiamando **SQLSpecialColumns**. (Per altre informazioni, vedere il supporto per **SQLSpecialColumns** con l'argomento *IdentifierType* impostato su SQL_BEST_ROWID come feature 20 nella [conformità dell'interfaccia Core](../../../odbc/reference/develop-app/core-interface-conformance.md)).|  
|209|Impostare l'attributo dell'istruzione SQL_ATTR_CONCURRENCY su almeno un valore diverso da SQL_CONCUR_READ_ONLY.|  
|210|Possibilità di timeout della richiesta di accesso e delle query SQL (SQL_ATTR_LOGIN_TIMEOUT e SQL_ATTR_QUERY_TIMEOUT).|  
|211|Possibilità di modificare il livello di isolamento predefinito; possibilità di eseguire transazioni con il livello di isolamento "serializzabile".|
