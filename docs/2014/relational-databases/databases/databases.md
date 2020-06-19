---
title: Database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- data warehouse [SQL Server]
- OLTP databases [SQL Server]
- databases [SQL Server], about databases
ms.assetid: 316eea58-81b8-4bf3-a1fc-801946740e94
author: stevestein
ms.author: sstein
ms.openlocfilehash: ea3da64ce6da8cbcb32b5854f14e8d24349c0c25
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970081"
---
# <a name="databases"></a>Database
  Un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è costituito da una raccolta di tabelle in cui è archiviato un set specifico di dati strutturati. Una tabella contiene una raccolta di righe, definite anche record o tuple, e colonne, definite anche attributi. Ogni colonna nella tabella è progettata per contenere un tipo di informazioni specifico, ad esempio date, nomi, importi in valuta e numeri.  
  
## <a name="basic-information-about-databases"></a>Informazioni di base sui database  
 Un computer può disporre di una o più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può contenere uno o più database.  All'interno di un database sono presenti uno o più gruppi di proprietà di oggetti denominati schemi. All'interno di ogni schema sono presenti oggetti di database quali tabelle, viste e stored procedure. Alcuni oggetti quali certificati e chiavi asimmetriche sono contenuti all'interno del database, ma non all'interno di uno schema. Per altre informazioni sulla creazione delle tabelle, vedere [Tabelle](../tables/tables.md).  
  
 I database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono archiviati in file del file system. I file possono essere raggruppati in filegroup. Per altre informazioni su file e filegroup, vedere [Filegroup e file di database](database-files-and-filegroups.md).  
  
 Quando un utente accede a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene identificato come account di accesso. Quando un utente accede a un database viene identificato come utente di database. Un utente di database può essere basato su un account di accesso. Se sono abilitati i database indipendenti, è possibile creare un utente di database non basato su un account di accesso. Per altre informazioni sugli utenti, vedere [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql).  
  
 A un utente che dispone di accesso a un database può essere fornita l'autorizzazione per accedere agli oggetti nel database. Sebbene sia possibile concedere autorizzazioni a singoli utenti, si consiglia di creare ruoli del database, aggiungere gli utenti del database ai ruoli, quindi concedere l'autorizzazione di accesso ai ruoli. La concessione di autorizzazioni ai ruoli anziché agli utenti agevola la coerenza e la comprensibilità delle autorizzazioni man mano che il numero di utenti aumenta e si modifica. Per altre informazioni sulle autorizzazioni per i ruoli, vedere [CREATE ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql) ed [Entità &#40;motore di database&#41;](../security/authentication-access/principals-database-engine.md).  
  
## <a name="working-with-databases"></a>Utilizzo dei database  
 La maggior parte degli utenti che operano con i database utilizza lo strumento [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . Lo strumento [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] dispone di un'interfaccia utente grafica per la creazione di database e degli oggetti nei database. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] usa anche un editor di query per interagire con i database scrivendo istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. È possibile installare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] dal disco dell'installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o scaricandolo da MSDN.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|||  
|-|-|  
|[Database di sistema](system-databases.md)|[Eliminare file di dati o file di log da un database](delete-data-or-log-files-from-a-database.md)|  
|[Database indipendenti](contained-databases.md)|[Visualizzare le informazioni sullo spazio allocato ai dati e ai log per un database](display-data-and-log-space-information-for-a-database.md)|  
|[File di dati di SQL Server in Azure](sql-server-data-files-in-microsoft-azure.md)|[Aumentare le dimensioni di un database](increase-the-size-of-a-database.md)|  
|[Filegroup e file di database](database-files-and-filegroups.md)|[Rinominare un database](rename-a-database.md)|  
|[Stati del database](database-states.md)|[Impostare un database in modalità utente singolo](set-a-database-to-single-user-mode.md)|  
|[Stati di file](file-states.md)|[Compattare un database](shrink-a-database.md)|  
|[Stima delle dimensioni di un database](estimate-the-size-of-a-database.md)|[Compattare un file](shrink-a-file.md)|  
|[Copiare database in altri server](copy-databases-to-other-servers.md)|[Visualizzare o modificare le proprietà di un database](view-or-change-the-properties-of-a-database.md)|  
|[Collegamento e scollegamento di un database &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)|[Visualizzare un elenco di database in un'istanza di SQL Server](view-a-list-of-databases-on-an-instance-of-sql-server.md)|  
|[Aggiungere file di dati o file di log a un database](add-data-or-log-files-to-a-database.md)|[Visualizzare o modificare il livello di compatibilità di un database](view-or-change-the-compatibility-level-of-a-database.md)|  
|[Modificare le impostazioni di configurazione per un database](change-the-configuration-settings-for-a-database.md)|[Utilizzare la Creazione guidata piano di manutenzione](../maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|[Creazione di un database](create-a-database.md)|[Creare un alias del tipo di dati definito dall'utente](create-a-user-defined-data-type-alias.md)|  
|[Eliminare un database](delete-a-database.md)|[Snapshot del database &#40;SQL Server&#41;](database-snapshots-sql-server.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
 [Indici](../indexes/indexes.md)  
  
 [Visualizzazioni](../views/views.md)  
  
 [Stored procedure &#40;Motore di database&#41;](../stored-procedures/stored-procedures-database-engine.md)  
  
  
