---
title: Eliminare uno snapshot del database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- removing database snapshots
- deleting database snapshots
- database snapshots [SQL Server], deleting
ms.assetid: ad70ec97-d5fb-41aa-b72a-915e74b61b76
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0738c1e661c679022a6a635af756003fdd98dfe0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68086019"
---
# <a name="drop-a-database-snapshot-transact-sql"></a>Eliminare uno snapshot del database (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La rimozione di uno snapshot del database comporta l'eliminazione dello snapshot da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nonché l'eliminazione dei file sparse da esso utilizzati. Quando si elimina uno snapshot del database, tutte le relative connessioni utente vengono interrotte.  
  
## <a name="security"></a>Security  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Uno snapshot del database può essere rimosso da qualsiasi utente che disponga delle autorizzazioni DROP DATABASE.  
  
##  <a name="how-to-drop-a-database-snapshot-using-transact-sql"></a><a name="TsqlProcedure"></a> Come eliminare uno snapshot del database (tramite Transact-SQL)  
 **Per eliminare uno snapshot del database**  
  
1.  Identificare lo snapshot del database da eliminare. È possibile visualizzare gli snapshot di un database in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Visualizzare uno snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md).  
  
2.  Eseguire un'istruzione [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md) , specificando il nome dello snapshot del database da eliminare. La sintassi è la seguente:  
  
     DROP DATABASE *database_snapshot_name* [ **,** ...*n* ]  
  
     Dove *database_snapshot_name* è il nome dello snapshot del database da eliminare.  
  
####  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Esempio (Transact-SQL)  
 Nell'esempio seguente viene rimosso uno snapshot di database, denominato SalesSnapshot0600, senza influire sul database di origine.  
  
```  
DROP DATABASE SalesSnapshot0600 ;  
```  
  
 Tutte le connessioni utente a SalesSnapshot0600 vengono terminate e tutti i file sparse del file system NTFS utilizzati dallo snapshot vengono eliminati.  
  
> [!NOTE]  
>  Per informazioni sull'uso di file sparse con gli snapshot del database, vedere [Snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Creare uno snapshot del database &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Visualizzazione di uno snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [Ripristinare un database a uno snapshot del database](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
  
## <a name="see-also"></a>Vedere anche  
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [Snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
