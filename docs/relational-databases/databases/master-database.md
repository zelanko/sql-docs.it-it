---
title: Database master | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], about
- master database [SQL Server]
ms.assetid: 660e909f-61eb-406b-bbce-8864dd629ba0
author: stevestein
ms.author: sstein
ms.openlocfilehash: e8c1447bfb5a4776430d24959267c7ec29aa48e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133598"
---
# <a name="master-database"></a>Database master

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Nel database **master** vengono registrate tutte le informazioni a livello di sistema relative a un sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . inclusi i metadati a livello globale dell'istanza quali gli account di accesso, gli endpoint, i server collegati e le impostazioni di configurazione di sistema. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], gli oggetti di sistema non sono più archiviati nel database **master** , ma sono archiviati nel [database Resource](../../relational-databases/databases/resource-database.md). Nel database **master** vengono inoltre registrate l'esistenza di tutti gli altri database e la posizione dei relativi file di database, nonché le informazioni di inizializzazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non è pertanto possibile avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se il database **master** non è disponibile.  

> [!IMPORTANT]
> Per i singoli database e i pool elastici di database SQL di Azure, si applicano solo il database master e il database tempdb. Per altre informazioni, vedere [Informazioni sul server di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-servers#what-is-an-azure-sql-database-server). Per una descrizione di tempdb nel contesto del database SQL di Azure, vedere [Database tempdb nel database SQL](tempdb-database.md#tempdb-database-in-sql-database). Per Istanza gestita di database SQL di Azure si applicano tutti i database di sistema. Per altre informazioni sulle istanze gestite nel database SQL di Azure, vedere [Informazioni su Istanza gestita](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)
  
## <a name="physical-properties-of-master"></a>Proprietà fisiche del database master

Nella tabella seguente sono illustrati i valori di configurazione iniziali dei file di dati e di log del database **master** per SQL Server e per Istanza gestita di database SQL di Azure. Le dimensioni di questi file possono variare leggermente a seconda dell'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|File|Nome logico|Nome fisico|Aumento di dimensioni del file|  
|----------|------------------|-------------------|-----------------|  
|Dati primari|master|master.mdf|Aumento automatico del 10% fino a quando il disco risulta pieno.|  
|File di log|mastlog|mastlog.ldf|Aumento automatico del 10% fino a un massimo di 2 terabyte.|  
  
Per informazioni su come spostare i file di dati e di log del database **master** , vedere [Spostare i database di sistema](../../relational-databases/databases/move-system-databases.md).  

> [!IMPORTANT]
> Per il server di database SQL di Azure, l'utente non ha alcun controllo sulle dimensioni del database **master**.
  
### <a name="database-options"></a>Opzioni di database

Nella tabella seguente è indicato il valore predefinito di ogni opzione del database **master** per SQL Server e per Istanza gestita di database SQL di Azure e viene specificato se il valore è modificabile. Per visualizzare le impostazioni correnti di queste opzioni, usare la vista del catalogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
> [!IMPORTANT]
> Per i database singoli e i pool elastici di database SQL di Azure, l'utente non ha alcun controllo su queste opzioni del database.

|Opzione di database|Valore predefinito|Modificabile|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|no|  
|ANSI_NULL_DEFAULT|OFF|Sì|  
|ANSI_NULLS|OFF|Sì|  
|ANSI_PADDING|OFF|Sì|  
|ANSI_WARNINGS|OFF|Sì|  
|ARITHABORT|OFF|Sì|  
|AUTO_CLOSE|OFF|no|  
|AUTO_CREATE_STATISTICS|ON|Sì|  
|AUTO_SHRINK|OFF|no|  
|AUTO_UPDATE_STATISTICS|ON|Sì|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sì|  
|CHANGE_TRACKING|OFF|no|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sì|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sì|  
|CURSOR_DEFAULT|GLOBAL|Sì|  
|Opzioni relative alla disponibilità del database|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|no<br /><br /> no<br /><br /> no|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sì|  
|DB_CHAINING|ON|no|  
|ENCRYPTION|OFF|no|  
|MIXED_PAGE_ALLOCATION|ON|no|  
|NUMERIC_ROUNDABORT|OFF|Sì|  
|PAGE_VERIFY|CHECKSUM|Sì|  
|PARAMETERIZATION|SIMPLE|Sì|  
|QUOTED_IDENTIFIER|OFF|Sì|  
|READ_COMMITTED_SNAPSHOT|OFF|no|  
|RECOVERY|SIMPLE|Sì|  
|RECURSIVE_TRIGGERS|OFF|Sì|  
|Opzioni relative a Service Broker|DISABLE_BROKER|no|  
|TRUSTWORTHY|OFF|Sì|  
  
Per una descrizione di queste opzioni di database, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="restrictions"></a>Restrictions  
Nel database **master** non è possibile eseguire le operazioni seguenti:  
  
- Aggiunta di file o di filegroup.  
- Modifica delle regole di confronto. Le regole di confronto predefinite corrispondono a quelle del server.  
- Modifica del proprietario del database. **master** è di proprietà di **sa**.  
- Creazione di un catalogo o di un indice full-text.  
- Creazione di trigger nelle tabelle di sistema del database.  
- Eliminazione del database.  
- Eliminazione dell'utente **guest** dal database.  
- Abilitazione dell'acquisizione dei dati delle modifiche.  
- Partecipazione al mirroring del database.  
- Rimozione del filegroup primario, del file di dati primario o del file di log.  
- Ridenominazione del filegroup primario o del database.  
- Impostazione del database su OFFLINE.  
- Impostazione del database o del filegroup primario su READ_ONLY.  
  
## <a name="recommendations"></a>Indicazioni  
Quando si utilizza il database **master** , è consigliabile attenersi alle indicazioni seguenti:  
  
- Tenere sempre a disposizione un backup aggiornato del database **master** .  
- Creare il prima possibile un backup del database **master** dopo aver eseguito le operazioni seguenti:  
  
  - Creazione, modifica o eliminazione di un database  
  - Modifica dei valori di configurazione di un server o di un database.  
  - Modifica o aggiunta di account di accesso.  
  
- Non creare oggetti utente nel database **master**. In caso contrario, sarà necessario creare backup del database **master** più frequenti.  
- Non impostare l'opzione TRUSTWORTHY su ON per il database **master** .  
  
## <a name="what-to-do-if-master-becomes-unusable"></a>Cosa fare se il database master diventa inutilizzabile  
 Se il database **master** diventa inutilizzabile, è possibile ripristinare uno stato utilizzabile del database in uno dei modi seguenti:  
  
- Ripristinare il database **master** da un backup del database corrente.  
  
  Se è possibile avviare l'istanza del server, dovrebbe essere possibile anche ripristinare il database **master** da un backup completo del database. Per altre informazioni, vedere [Ripristinare il database master &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md).  
  
- Ricompilare il database **master** da zero.  
  
  Se non è possibile avviare **in seguito a gravi danni al database** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario ricompilare il database **master**. Per altre informazioni, vedere [Ricompilare database di sistema](../../relational-databases/databases/rebuild-system-databases.md).  
  
  > [!IMPORTANT]  
  >  La ricompilazione del database **master** comporta la ricompilazione di tutti i database di sistema.  
  
## <a name="related-content"></a>Contenuto correlato  
- [Ricompilare database di sistema](../../relational-databases/databases/rebuild-system-databases.md)  
- [Database di sistema.](../../relational-databases/databases/system-databases.md)  
- [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
- [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
- [Spostare file del database](../../relational-databases/databases/move-database-files.md)  
