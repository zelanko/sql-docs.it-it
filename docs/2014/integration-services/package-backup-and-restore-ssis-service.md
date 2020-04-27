---
title: Backup e ripristino di pacchetti (servizio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, backup and restore
- backing up packages [Integration Services]
- packages [Integration Services], backup and restore
- SQL Server Integration Services packages, backup and restore
- restoring packages [Integration Services]
- Integration Services packages, backup and restore
ms.assetid: c67d3b83-a6c8-40de-920f-9236de4ac87f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b5c775393f7815084e8a79aae4be7f0974886f3e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66056926"
---
# <a name="package-backup-and-restore-ssis-service"></a>Backup e ripristino di pacchetti (servizio SSIS)
    
> [!IMPORTANT]  
>  In questo argomento viene illustrato il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , un servizio Windows per la gestione dei pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] supporta il servizio per la compatibilità con le versioni precedenti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A partire da [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], è possibile gestire oggetti come i pacchetti del server Integration Services.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] i pacchetti possono essere salvati nel file System o in msdb, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] un database di sistema. È possibile eseguire il backup e il ripristino dei pacchetti salvati in msdb usando le funzionalità di backup e ripristino di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Per altre informazioni sul backup e sul ripristino del database msdb, fare clic su uno degli argomenti seguenti:  
  
-   [Backup e ripristino di database SQL Server](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [Backup e ripristino di database di sistema &#40;SQL Server&#41;](../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] include l'utilità del prompt dei comandi **dtutil** (dtutil.exec), che può essere usata per gestire i pacchetti. Per altre informazioni, vedere [dtutil Utility](dtutil-utility.md).  
  
## <a name="configuration-files"></a>File di configurazione  
 I file di configurazione dei pacchetti vengono archiviati nel file system. Questi file non vengono tuttavia inclusi nel backup del database msdb. Di conseguenza, è necessario assicurarsi che il backup di questi file venga eseguito regolarmente nell'ambito del piano per la sicurezza dei pacchetti salvati in msdb. Per includere configurazioni nel backup del database msdb, è consigliabile usare il tipo di configurazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] invece delle configurazioni basate su file.  
  
## <a name="packages-stored-in-the-file-system"></a>Pacchetti archiviati nel file system  
 Nel piano per il backup del file system del server deve essere incluso il backup dei pacchetti salvati nel file system. Nel file di configurazione del servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , il cui nome predefinito è MsDtsSrvr.ini.xml, sono elencate le cartelle del server di cui il servizio esegue il monitoraggio. Assicurarsi di eseguire il backup di queste cartelle. I pacchetti potrebbero essere archiviati in altre cartelle del server. Assicurarsi di includere nel backup anche queste cartelle.  
  
  
