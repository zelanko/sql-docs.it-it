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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bff3de6a9b9ec57f1ea96d6db17b9b30c5a22996
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515315"
---
# <a name="level-2-interface-conformance"></a>Conformità di interfaccia di livello 2
Il livello di conformità di interfaccia di livello 2 include la funzionalità di conformità a livello dell'interfaccia di livello 1 oltre alle funzionalità seguenti:  
  
|||  
|-|-|  
|201|Usare nomi in tre parti delle tabelle di database e delle visualizzazioni. (Per altre informazioni, vedere le due parti denominazione funzionalità supporto 101 nella [conformità di interfaccia di livello 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md).)|  
|202|Vengono descritti i parametri dinamici, chiamando **SQLDescribeParam**.|  
|203|Utilizzare non solo i parametri di input, ma anche i parametri di output e input/output e valori di risultato delle stored procedure.|  
|204|Usare i segnalibri, incluso il recupero di segnalibri, chiamando **SQLDescribeCol** e **SQLColAttribute** nella colonna il numero 0; il recupero basato su un segnalibro, chiamando **SQLFetchScroll** con il *FetchOrientation* argomento impostato su SQL_FETCH_BOOKMARK; e update, delete e per il recupero da operazioni di segnalibro, chiamando **SQLBulkOperations** con la *Operazione* argomento impostato su SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK o SQL_FETCH_BY_BOOKMARK.|  
|205|Recuperare informazioni avanzate sul dizionario dei dati, chiamando **SQLColumnPrivileges**, **SQLForeignKeys**, e **SQLTablePrivileges**.|  
|206|Usare funzioni ODBC invece delle istruzioni SQL per eseguire operazioni di database aggiuntive chiamando **SQLBulkOperations** con SQL_ADD, o **SQLSetPos** con SQL_DELETE o SQL_UPDATE. (Supporto per le chiamate a **SQLSetPos** con il *LockType* argomento impostato su SQL_LOCK_EXCLUSIVE o SQL_LOCK_UNLOCK non fa parte dei livelli di conformità, ma è una funzionalità facoltativa.)|  
|207|Abilitare l'esecuzione asincrona delle funzioni ODBC per le singole istruzioni specificate.|  
|208|Ottenere la colonna SQL_ROWVER identificazione delle righe delle tabelle, chiamando **SQLSpecialColumns**. (Per altre informazioni, vedere il supporto per **SQLSpecialColumns** con il *IdentifierType* argomento impostato su SQL_BEST_ROWID come funzionalità 20 nel [conformità di interfaccia Core](../../../odbc/reference/develop-app/core-interface-conformance.md) .)|  
|209|Impostare l'attributo di istruzione SQL_ATTR_CONCURRENCY su almeno un valore diverso da SQL_CONCUR_READ_ONLY.|  
|210|La possibilità di raggiungere il timeout richiesta di accesso e le query SQL (SQL_ATTR_LOGIN_TIMEOUT e SQL_ATTR_QUERY_TIMEOUT).|  
|211|La possibilità di modificare il livello di isolamento predefinito; la possibilità di eseguire transazioni con il livello di isolamento "serializzabile".|
