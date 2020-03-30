---
title: Modificare le impostazioni di configurazione per un database | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- database configuration [SQL Server]
- configuration options [SQL Server], databases
- modifying database configuration settings
ms.assetid: c29c3385-5043-400f-bb4e-044a4c9a9a4b
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 59162df3f9a28beb5273a4e94768588dc53714fc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68137390"
---
# <a name="change-the-configuration-settings-for-a-database"></a>Modificare le impostazioni di configurazione per un database
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In questo argomento si illustra come modificare le opzioni a livello di database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Queste opzioni sono specifiche di ogni database e non hanno effetto su altri database.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per modificare le opzioni di configurazione per un database usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Queste opzioni possono essere modificate solo dall'amministratore di sistema, dal proprietario del database, dai membri dei ruoli predefiniti del server **sysadmin** e **dbcreator** e dai membri del ruolo predefinito del database **db_owner** .  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per il database.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-change-the-option-settings-for-a-database"></a>Per modificare le opzioni di configurazione per un database  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , espandere il server, espandere **Database**, fare clic con il pulsante destro del mouse su un database e quindi scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo **Proprietà database** fare clic su **Opzioni** per accedere alla maggior parte delle impostazioni di configurazione. Le configurazioni di file, filegroup, mirroring e log shipping sono disponibili nelle rispettive pagine.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-change-the-option-settings-for-a-database"></a>Per modificare le opzioni di configurazione per un database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si impostano le opzioni relative al modello di recupero e alla verifica delle pagine di dati per il database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
 [!code-sql[DatabaseDDL#AlterDatabase7](../../relational-databases/databases/codesnippet/tsql/change-the-configuration_1.sql)]  
  
 Per altri esempi, vedere [Opzioni di ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Mirroring del database di ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [Rinominare un database](../../relational-databases/databases/rename-a-database.md)   
 [Compattare un database](../../relational-databases/databases/shrink-a-database.md)  
  
  
