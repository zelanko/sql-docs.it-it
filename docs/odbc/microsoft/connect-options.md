---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06695bf1770c9e362decac5702dcd924d47c23bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301768"
---
# <a name="connect-options"></a>Opzioni di connessione
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Queste opzioni consentono di personalizzare la connessione al database all'interno di un'applicazione.  
  
|Opzione di connessione|Note|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|Se si sceglie SQL_AUTOCOMMIT_OFF, l'applicazione deve esplicitamente eseguire il commit o il rollback delle transazioni con [SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md).|  
|SQL_ODBC_CURSORS|Questo attributo di connessione viene implementato in Gestione Driver.|  
|SQL_OPT_TRACE|Questo attributo di connessione viene implementato in Gestione Driver.|  
|SQL_OPT_TRACEFILE|Questo attributo di connessione viene implementato in Gestione Driver.|  
|SQL_TRANSLATE_DLL|Restituisce l'errore: "Driver non valido."|  
|SQL_TRANSLATE_OPTION|La DLL di conversione passato un valore a 32 bit.|  
|SQL_TXN_ISOLATION|Il driver consente solo SQL_TXN_READ_COMMITTED.<br /><br /> Non sono supportati i vParams seguenti:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|Questo attributo di connessione ODBC 3.0 consente di utilizzare il Driver ODBC per Oracle nelle transazioni distribuite coordinate da Servizi componenti Microsoft (o MTS, se si utilizza Windows NT). Fornisce il puntatore all'interfaccia *pITransaction* alla transazione come le *vParam* argomento.|  
|SQL_ATTR_CONNECTION_DEAD|Questo attributo di connessione ODBC 3.5 di sola lettura consente di determinare se la connessione al server Oracle non è riuscito. Introduzione di sola lettura. non è possibile impostare.|
