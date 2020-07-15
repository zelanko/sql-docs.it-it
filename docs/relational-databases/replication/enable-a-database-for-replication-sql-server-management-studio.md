---
title: Abilitare un database per la replica (SSMS)
description: Informazioni su come abilitare un database per la replica usando SQL Server Management Studio (SSMS) o Transact-SQL (T-SQL).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 470db784550df51193337aefd8a81360563d2bc3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85653444"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>Abilitazione di un database per la replica (SQL Server Management Studio)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  
Un database viene implicitamente abilitato per la replica quando un membro del ruolo predefinito del server **sysadmin** crea una pubblicazione mediante la Creazione guidata nuova pubblicazione. Il membro del ruolo predefinito del server **sysadmin** può inoltre abilitare esplicitamente un database per la replica, in modo che un membro del ruolo predefinito del database **db_owner** possa creare una o più pubblicazioni in tale database. A tale scopo, usare la pagina **Database di pubblicazione** della finestra di dialogo **Proprietà server di pubblicazione - \<Publisher>** . Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
## <a name="using-sql-server-management-studio-ssms"></a>Utilizzo di SQL Server Management Studio (SSMS)
  
1.  Nella pagina **Database di pubblicazione** della finestra di dialogo **Proprietà server di pubblicazione - \<Publisher>** selezionare la casella di controllo **Transazionale** e/o **Merge** per ogni database da replicare. Selezionare **Transazionale** per abilitare il database per la replica snapshot.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
## <a name="using-transact-sql-t-sql"></a>Uso di Transact-SQL (T-SQL)
È possibile abilitare un database per la replica con il codice Transact-SQL seguente: 

```sql
USE master
EXEC sp_replicationdboption @dbname = 'AdventureWorks2017',
@optname = 'publish',
@value = 'true'
GO
```

Per disabilitare la pubblicazione, impostare @value = 'false'. 
