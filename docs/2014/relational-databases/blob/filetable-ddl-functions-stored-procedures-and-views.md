---
title: DDL, funzioni, stored procedure e viste FileTable | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 85e0c761f5dc784698b3aed361ce50488a93e366
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66010095"
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>DDL FileTable, funzioni, stored Procedure e viste
  Vengono elencate le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] e gli oggetti di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aggiunti o modificati per supportare la funzionalità FileTable in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La colonna Stato nelle tabelle seguenti indica se l'elemento è nuovo in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o è presente nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ma è stato modificato in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] per supportare la ricerca semantica.  
  
 Per l'elenco di istruzioni e oggetti di database che supportano FILESTREAM, vedere [FILESTREAM DDL, Functions, Stored Procedures, and Views](../views/views.md).  
  
##  <a name="transact-sql-data-definition-language-ddl-statements"></a><a name="ddl"></a> Istruzioni Transact-SQL DDL (Data Definition Language)  
  
|Oggetto|Stato|Altre informazioni|  
|------------|------------|----------------------|  
|[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)<br /><br /> [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)|Modificato|[Abilitare i prerequisiti per la tabella FileTable](enable-the-prerequisites-for-filetable.md)<br /><br /> [Gestire tabelle FileTable](manage-filetables.md)|  
|[ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)|Modificato|[Creare, modificare ed eliminare FileTable](create-alter-and-drop-filetables.md)<br /><br /> [Gestire tabelle FileTable](manage-filetables.md)|  
|[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)|Modificato|[Abilitare i prerequisiti per la tabella FileTable](enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)|Modificato|[Creare, modificare ed eliminare FileTable](create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)<br /><br /> [Argomenti RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)|Modificato||  
  
##  <a name="functions"></a><a name="func"></a> Funzioni  
  
|Oggetto|Stato|Altre informazioni|  
|------------|------------|----------------------|  
|[FileTableRootPath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filetablerootpath-transact-sql)|**Aggiunto**|[Usare directory e percorsi in FileTable](work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql)|**Aggiunto**|[Usare directory e percorsi in FileTable](work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql)|**Aggiunto**|[Usare directory e percorsi in FileTable](work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="stored-procedures"></a><a name="sproc"></a> Stored procedure  
  
|Oggetto|Stato|Altre informazioni|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles)|**Aggiunto**|[Gestire tabelle FileTable](manage-filetables.md)|  
  
##  <a name="catalog-views"></a><a name="cv"></a> Viste del catalogo  
  
|Oggetto|Stato|Altre informazioni|  
|------------|------------|----------------------|  
|[sys.database_filestream_options &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql)|**Aggiunto**|[Abilitare i prerequisiti per la tabella FileTable](enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql)|**Aggiunto**|[Creare, modificare ed eliminare FileTable](create-alter-and-drop-filetables.md)<br /><br /> [Gestire tabelle FileTable](manage-filetables.md)|  
|[sys.filetables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetables-transact-sql)|**Aggiunto**|[Gestire tabelle FileTable](manage-filetables.md)|  
|[sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|Modificato|[Gestire tabelle FileTable](manage-filetables.md)|  
  
##  <a name="dynamic-management-views"></a><a name="dmv"></a> DMV  
  
|Oggetto|Stato|Altre informazioni|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql)|**Aggiunto**|[Gestire tabelle FileTable](manage-filetables.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire tabelle FileTable](manage-filetables.md)  
  
  
