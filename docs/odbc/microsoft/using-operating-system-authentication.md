---
description: Uso dell'autenticazione del sistema operativo
title: Uso dell'autenticazione del sistema operativo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94563fee00c979addb6fc088bfb3881763e4d188
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471323"
---
# <a name="using-operating-system-authentication"></a>Uso dell'autenticazione del sistema operativo
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 L'autenticazione del sistema operativo Oracle si basa sul sistema operativo sottostante per controllare l'accesso agli account di database. Quando si usa questo tipo di account di accesso, gli utenti non devono immettere una password.  
  
 Per sfruttare i vantaggi di questa funzionalità, specificare "/" come ID utente e non specificare una password per la connessione utilizzando una delle seguenti API di connessione: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)o [SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 I database Oracle utilizzano i servizi di autenticazione SQL * NET per autenticare gli utenti connessi. Questo servizio funziona bene se gli utenti sono connessi a Oracle tramite sqlplus; Tuttavia, quando l'utente connesso è un servizio, ad esempio Internet Information Services, l'autenticazione ha esito negativo. Si tratta di un limite noto dell' \* autenticazione di SQL NET e viene generato l'errore seguente: "[Microsoft] [driver ODBC per Oracle] [Oracle] ora-12641: TNS: Impossibile inizializzare il servizio di autenticazione."  
  
 È possibile risolvere il problema modificando il file SQLNET. ora. Questo file di configurazione viene in genere archiviato nella sottodirectory Network\Admin della Home directory di Oracle. Aggiungere la riga seguente a SQLNET. ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
