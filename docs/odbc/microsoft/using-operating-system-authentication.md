---
title: Usa l'autenticazione del sistema operativo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a532c253ea2204fa3636c24c503cbefd3fa6311
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127816"
---
# <a name="using-operating-system-authentication"></a>Uso dell'autenticazione del sistema operativo
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Autenticazione del sistema operativo Oracle si basa sul sistema operativo sottostante per controllare l'accesso agli account di database. Gli utenti non devono immettere una password quando si usa questo tipo di account di accesso.  
  
 Per sfruttare i vantaggi di questa funzionalità, specificare "/" come l'ID utente e non si specifica una password quando ci si connette utilizzando una della connessione API seguente: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md), o [SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 Oracle database usano SQL * Net i servizi di autenticazione per autenticare gli utenti sono connessi. Questo servizio funziona anche se gli utenti sono connessi a Oracle tramite SQLPlus; Tuttavia, quando l'utente ha eseguito l'accesso è un servizio, ad esempio Internet Information Services, l'autenticazione ha esito negativo. Si tratta di una limitazione nota del SQL\*autenticazione Net e produce il seguente errore: "[Microsoft] [driver ODBC per Oracle] [Oracle] ORA-12641: Servizio TNS:Authentication inizializzazione non riuscita."  
  
 È possibile correggere il problema modificando il file SQLNET. Questo file di configurazione è in genere archiviato nella sottodirectory Network\Admin della home directory Oracle. Aggiungere la riga seguente a SQLNET:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
