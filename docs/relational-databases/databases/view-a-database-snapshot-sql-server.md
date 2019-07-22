---
title: Visualizzare uno snapshot del database (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], viewing
- displaying database snapshots
- viewing database snapshots
ms.assetid: 123f19b2-0850-4033-8507-59ebdfb368ee
author: stevestein
ms.author: sstein
ms.openlocfilehash: 57df1a271d7c7694de048864f8b0db06223c4009
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127097"
---
# <a name="view-a-database-snapshot-sql-server"></a>Visualizzazione di uno snapshot del database (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene illustrato come visualizzare uno snapshot del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  Per creare, ripristinare o eliminare uno snapshot del database, è necessario utilizzare [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Per visualizzare uno snapshot del database mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per visualizzare uno snapshot del database**  
  
1.  In Esplora oggetti connettersi all'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere l'istanza in questione.  
  
2.  Espandere **Database.**  
  
3.  Espandere **Snapshot database**e selezionare lo snapshot da visualizzare.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per visualizzare uno snapshot del database**  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Per elencare gli snapshot del database dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], eseguire una query sulla colonna **source_database_id** della vista del catalogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) per valori non NULL.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Creare uno snapshot del database &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Ripristinare un database a uno snapshot del database](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
-   [Eliminare uno snapshot del database &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
