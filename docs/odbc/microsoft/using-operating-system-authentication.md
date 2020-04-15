---
title: Utilizzo dell'autenticazione del sistema operativo Documenti Microsoft
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
ms.openlocfilehash: d6520202bdbc31baf1156531457cb70a98656e88
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292841"
---
# <a name="using-operating-system-authentication"></a>Uso dell'autenticazione del sistema operativo
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 L'autenticazione del sistema operativo Oracle si basa sul sistema operativo sottostante per controllare l'accesso agli account di database. Gli utenti non devono immettere una password quando utilizzano questo tipo di login.  
  
 Per sfruttare questa funzionalità, specificare "/" come ID utente e non specificare una password per la connessione utilizzando una delle seguenti API di connessione: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)o [SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 I database Oracle utilizzano i servizi di autenticazione di SQL-Net per autenticare gli utenti connessi. Questo servizio funziona bene se gli utenti sono connessi a Oracle tramite SQLPlus; Tuttavia, quando l'utente connesso è un servizio come Internet Information Services, l'autenticazione non riesce. Si tratta di una\*limitazione nota dell'autenticazione di rete SQL e genera il seguente errore: "[Microsoft][ODBC driver for Oracle][Oracle]ORA-12641: TNS:authentication service failed to initialize."  
  
 È possibile risolvere il problema modificando il file Sqlnet.ora. Questo file di configurazione viene in genere memorizzato nella sottodirectory Rete/Amministrazione della home directory Oracle. Aggiungere la riga seguente a Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
