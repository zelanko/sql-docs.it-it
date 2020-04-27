---
title: Database master | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], about
- master database [SQL Server]
ms.assetid: 660e909f-61eb-406b-bbce-8864dd629ba0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 767d77eefe8c54fe5a3d584c670cc991b284178e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62917044"
---
# <a name="master-database"></a>Database master
  Nel database **master** vengono registrate tutte le informazioni a livello di sistema relative a un sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . inclusi i metadati a livello globale dell'istanza quali gli account di accesso, gli endpoint, i server collegati e le impostazioni di configurazione di sistema. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], gli oggetti di sistema non sono più archiviati nel database **master** , ma sono archiviati nel [database Resource](resource-database.md). Nel database **master** vengono inoltre registrate l'esistenza di tutti gli altri database e la posizione dei relativi file di database, nonché le informazioni di inizializzazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non è pertanto possibile avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se il database **master** non è disponibile.  
  
## <a name="physical-properties-of-master"></a>Proprietà fisiche del database master  
 Nella tabella seguente sono illustrati i valori di configurazione iniziali dei file di dati e di log del database **master** . Le dimensioni di questi file possono variare leggermente a seconda dell'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|File|Nome logico|Nome fisico|Aumento di dimensioni del file|  
|----------|------------------|-------------------|-----------------|  
|Dati primari|master|master.mdf|Aumento automatico del 10% fino a quando il disco risulta pieno.|  
|File di log|mastlog|mastlog.ldf|Aumento automatico del 10% fino a un massimo di 2 terabyte.|  
  
 Per informazioni su come spostare i file di dati e di log del database **master** , vedere [Spostare i database di sistema](system-databases.md).  
  
### <a name="database-options"></a>Opzioni di database  
 Nella tabella seguente è illustrato il valore predefinito di ogni opzione del database **master** e viene specificato se il valore è modificabile. Per visualizzare le impostazioni correnti di queste opzioni, usare la vista del catalogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
|Opzione di database|Valore predefinito|Modificabile|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|No|  
|ANSI_NULL_DEFAULT|OFF|Sì|  
|ANSI_NULLS|OFF|Sì|  
|ANSI_PADDING|OFF|Sì|  
|ANSI_WARNINGS|OFF|Sì|  
|ARITHABORT|OFF|Sì|  
|AUTO_CLOSE|OFF|No|  
|AUTO_CREATE_STATISTICS|ON|Sì|  
|AUTO_SHRINK|OFF|No|  
|AUTO_UPDATE_STATISTICS|ON|Sì|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sì|  
|CHANGE_TRACKING|OFF|No|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sì|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sì|  
|CURSOR_DEFAULT|GLOBAL|Sì|  
|Opzioni relative alla disponibilità del database|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|No<br /><br /> No<br /><br /> No|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sì|  
|DB_CHAINING|ON|No|  
|ENCRYPTION|OFF|No|  
|NUMERIC_ROUNDABORT|OFF|Sì|  
|PAGE_VERIFY|CHECKSUM|Sì|  
|PARAMETERIZATION|SEMPLICE|Sì|  
|QUOTED_IDENTIFIER|OFF|Sì|  
|READ_COMMITTED_SNAPSHOT|OFF|No|  
|RECOVERY|SEMPLICE|Sì|  
|RECURSIVE_TRIGGERS|OFF|Sì|  
|Opzioni relative a Service Broker|DISABLE_BROKER|No|  
|TRUSTWORTHY|OFF|Sì|  
  
 Per una descrizione di queste opzioni di database, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
## <a name="restrictions"></a>Restrizioni  
 Nel database **master** non è possibile eseguire le operazioni seguenti:  
  
-   Aggiunta di file o di filegroup.  
  
-   Modifica delle regole di confronto. Le regole di confronto predefinite corrispondono a quelle del server.  
  
-   Modifica del proprietario del database. **master** è di proprietà di **sa**.  
  
-   Creazione di un catalogo o di un indice full-text.  
  
-   Creazione di trigger nelle tabelle di sistema del database.  
  
-   Eliminazione del database.  
  
-   Eliminazione dell'utente **Guest** dal database.  
  
-   Abilitazione dell'acquisizione dei dati delle modifiche.  
  
-   Partecipazione al mirroring del database.  
  
-   Rimozione del filegroup primario, del file di dati primario o del file di log.  
  
-   Ridenominazione del filegroup primario o del database.  
  
-   Impostazione del database su OFFLINE.  
  
-   Impostazione del database o del filegroup primario su READ_ONLY.  
  
## <a name="recommendations"></a>Consigli  
 Quando si utilizza il database **master** , è consigliabile attenersi alle indicazioni seguenti:  
  
-   Tenere sempre a disposizione un backup aggiornato del database **master** .  
  
-   Creare il prima possibile un backup del database **master** dopo aver eseguito le operazioni seguenti:  
  
    -   Creazione, modifica o eliminazione di un database  
  
    -   Modifica dei valori di configurazione di un server o di un database.  
  
    -   Modifica o aggiunta di account di accesso.  
  
-   Non creare oggetti utente nel database **master**. In caso contrario, sarà necessario creare backup del database **master** più frequenti.  
  
-   Non impostare l'opzione TRUSTWORTHY su ON per il database **master** .  
  
## <a name="what-to-do-if-master-becomes-unusable"></a>Cosa fare se il database master diventa inutilizzabile  
 Se il database **master** diventa inutilizzabile, è possibile ripristinare uno stato utilizzabile del database in uno dei modi seguenti:  
  
-   Ripristinare il database **master** da un backup del database corrente.  
  
     Se è possibile avviare l'istanza del server, dovrebbe essere possibile anche ripristinare il database **master** da un backup completo del database. Per altre informazioni, vedere [Ripristinare il database master &#40;Transact-SQL&#41;](../backup-restore/restore-the-master-database-transact-sql.md).  
  
-   Ricompilare il database **master** da zero.  
  
     Se non è possibile avviare **in seguito a gravi danni al database** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario ricompilare il database **master**. Per altre informazioni, vedere [Ricompilare database di sistema](rebuild-system-databases.md).  
  
    > [!IMPORTANT]  
    >  La ricompilazione del database **master** comporta la ricompilazione di tutti i database di sistema.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Ricompilare database di sistema](rebuild-system-databases.md)  
  
 [Database di sistema](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [Spostare file del database](move-database-files.md)  
  
  
