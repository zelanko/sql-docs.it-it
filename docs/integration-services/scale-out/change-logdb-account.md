---
title: Modificare l'account per la registrazione di SSIS Scale Out | Microsoft Docs
description: Questo articolo descrive come modificare l'account utente per la registrazione SSIS Scale Out
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 92cf3e13f1e386a77ba4621b817567af95b42884
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "67896979"
---
# <a name="change-the-account-for-scale-out-logging"></a>Modificare l'account per la registrazione di Scale Out

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
