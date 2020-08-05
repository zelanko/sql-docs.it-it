---
title: Modificare l'account per la registrazione di SSIS Scale Out | Microsoft Docs
description: Informazioni su come modificare l'account usato per la registrazione di SQL Server Integration Services (SSIS) Scale Out.
ms.custom: performance
ms.date: 06/29/2020
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.reviewer: maghan
ms.openlocfilehash: c53a389541408080f1de43da409b4b61ca85a0ec
ms.sourcegitcommit: 7035d9471876c70b99c58bf9b46af5cce6e9c66c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2020
ms.locfileid: "87522335"
---
# <a name="change-the-account-for-scale-out-logging"></a>Modificare l'account per la registrazione di Scale Out

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Durante l'esecuzione di pacchetti SSIS in Scale Out, i messaggi di evento vengono registrati nel database SSISDB con un account utente creato automaticamente, denominato **##MS_SSISLogDBWorkerAgentLogin##** . L'account di accesso dell'utente usa l'autenticazione di SQL Server.

Se si vuole modificare l'account usato per la registrazione in Scale Out, eseguire le operazioni seguenti:

> [!NOTE]
> Se si usa un account utente di Windows per la registrazione, usare lo stesso account che esegue il servizio Scale Out Worker. In caso contrario, l'accesso a SQL Server non riesce.

## <a name="1-create-a-user-for-ssisdb"></a>1. Creare un utente di SSISDB
Per istruzioni sulla creazione di un utente del database, vedere [Creare un utente di database](../../relational-databases/security/authentication-access/create-a-database-user.md).

## <a name="2-add-the-user-to-the-database-role-ssis_cluster_worker"></a>2. Aggiungere l'utente al ruolo del database ssis_cluster_worker

Per istruzioni sull'aggiunta di un ruolo del database, vedere [Aggiungere un ruolo](../../relational-databases/security/authentication-access/join-a-role.md).

## <a name="3-update-the-logging-information-in-ssisdb"></a>3. Aggiornare le informazioni di registrazione in SSISDB
Chiamare la stored procedure `[catalog].[update_logdb_info]` con la stringa del nome del server SQL Server e la stringa di connessione come parametri, come illustrato nell'esempio seguente:

```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-the-scale-out-worker-service"></a>4. Riavviare il servizio Scale Out Worker
Riavviare il servizio Scale Out Worker per rendere effettiva la modifica.

## <a name="next-steps"></a>Passaggi successivi
-   [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md)
