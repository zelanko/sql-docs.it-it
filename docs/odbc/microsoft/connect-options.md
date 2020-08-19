---
description: Opzioni di connessione
title: Opzioni di connessione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22326ca650f575c6a4f0503093306d8b68581475
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483684"
---
# <a name="connect-options"></a>Opzioni di connessione
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Queste opzioni consentono la personalizzazione della connessione del database all'interno di un'applicazione.  
  
|Opzione Connect|Note|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|Se si sceglie SQL_AUTOCOMMIT_OFF, l'applicazione deve eseguire il commit o il rollback delle transazioni in modo esplicito con [SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md).|  
|SQL_ODBC_CURSORS|Questo attributo di connessione viene implementato in Gestione driver.|  
|SQL_OPT_TRACE|Questo attributo di connessione viene implementato in Gestione driver.|  
|SQL_OPT_TRACEFILE|Questo attributo di connessione viene implementato in Gestione driver.|  
|SQL_TRANSLATE_DLL|Restituisce l'errore: "driver non in grado di supportare".|  
|SQL_TRANSLATE_OPTION|Valore a 32 bit passato al file Translation. dll.|  
|SQL_TXN_ISOLATION|Il driver consente solo SQL_TXN_READ_COMMITTED.<br /><br /> Gli vParams seguenti non sono supportati:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|Questo attributo di connessione ODBC 3,0 consente di utilizzare il driver ODBC per Oracle nelle transazioni distribuite coordinate da Microsoft Component Services (o MTS, se si utilizza Windows NT). Fornisce il puntatore all'interfaccia *pITransaction* alla transazione come argomento *parametro vParam* .|  
|SQL_ATTR_CONNECTION_DEAD|Questo attributo di connessione ODBC 3,5 di sola lettura consente di determinare se la connessione al server Oracle non è riuscita. Solo Get; non è possibile impostare.|
