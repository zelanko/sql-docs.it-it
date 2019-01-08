---
title: Eliminare file di dati o file di log da un database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], files
- deleting files
- removing files
- removing data
- data deletions [SQL Server]
- file deletion [SQL Server]
- deleting data
ms.assetid: 0db4018c-ce2c-4ba1-bb29-1e4f3791c925
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e0f2de1f7003e61dbdc8e82f7a9b549fd42c77fc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52783438"
---
# <a name="delete-data-or-log-files-from-a-database"></a>Eliminare file di dati o file di log da un database
  In questo argomento si descrive come eliminare file di dati o di log in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   Per poter essere eliminato, un file deve essere vuoto. Per altre informazioni, vedere [Compattare un file](shrink-a-file.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È richiesta l'autorizzazione ALTER per il database.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-delete-data-or-log-files-from-a-database"></a>Per eliminare file di dati o di log da un database  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
  
2.  Espandere **Database**, fare clic con il pulsante destro del mouse sul database da cui eliminare il file e quindi scegliere **Proprietà**.  
  
3.  Selezionare la pagina **File** .  
  
4.  Nella griglia **File di database** selezionare il file da eliminare, quindi fare clic su **Rimuovi**.  
  
5.  Fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-delete-data-or-log-files-from-a-database"></a>Per eliminare file di dati o di log da un database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**. In questo esempio si rimuove il file `test1dat4`.  
  
 [!code-sql[DatabaseDDL#AlterDatabase4](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase4)]  
  
 Per altri esempi, vedere [Opzioni per file e filegroup ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options).  
  
## <a name="see-also"></a>Vedere anche  
 [Compattare un database](shrink-a-database.md)   
 [Aggiungere file di dati o file di log a un database](add-data-or-log-files-to-a-database.md)  
  
  
