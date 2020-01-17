---
title: Eseguire script durante la sincronizzazione (SP di replica)
description: Informazioni su come usare le stored procedure di replica per eseguire script su richiesta durante il processo di sincronizzazione di una pubblicazione transazionale o di tipo merge.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d1027e969c12f5b5234f05bfeef12c7b93e3de84
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321721"
---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>Esecuzione di script durante la sincronizzazione (programmazione Transact-SQL della replica)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replica supporta l'esecuzione di script su richiesta per i Sottoscrittori di pubblicazioni transazionali e di tipo merge. Con questa funzionalità lo script viene copiato nella directory di lavoro della replica e quindi viene applicato al Sottoscrittore tramite **sqlcmd** . Per impostazione predefinita, se si verifica un errore durante l'applicazione dello script per una sottoscrizione di una pubblicazione transazionale, l'agente di distribuzione verrà arrestato. È possibile specificare uno script [!INCLUDE[tsql](../../includes/tsql-md.md)] da eseguire a livello di programmazione tramite le stored procedure di replica.  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>Per specificare uno script da eseguire per tutti i Sottoscrittori di una pubblicazione snapshot, transazionale o di tipo merge  
  
1.  Comporre e testare lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] che verrà eseguito su richiesta.  
  
2.  Salvare il file script in un percorso in cui sia accessibile all'agente snapshot per la pubblicazione.  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addscriptexec &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md). Specificare `@publication`, il nome del file script con il percorso UNC completo creato nel passaggio 2 per `@scriptfile` e uno dei valori seguenti per `@skiperror`:  
  
    -   **0** : l'agente arresterà l'esecuzione dello script se viene rilevato un errore.  
  
    -   **1** : l'agente registrerà gli errori e continuerà l'esecuzione dello script quando vengono rilevati errori.  
  
4.  Lo script specificato verrà eseguito in ogni Sottoscrittore la volta successiva che l'agente verrà eseguito per sincronizzare la sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Sincronizzare i dati](../../relational-databases/replication/synchronize-data.md)  
  
  
