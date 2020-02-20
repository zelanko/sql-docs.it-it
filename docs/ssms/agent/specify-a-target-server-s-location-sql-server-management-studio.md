---
title: Specificare la posizione di un server di destinazione
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], location
ms.assetid: 511ff311-21f5-4f2f-839f-b4deee26ec98
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ad1eb886c611da105be9c999d8ebc323edb9eb6d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75245796"
---
# <a name="specify-a-target-server39s-location"></a>Specificare la posizione di un server di destinazione
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene illustrato come specificare il percorso di un server di destinazione in una configurazione di amministrazione multiserver in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Restrictions"></a>Limitazioni e restrizioni  
L'esecuzione di questa azione modifica il Registro di sistema. La modifica manuale del Registro di sistema non è un'operazione consigliata, in quanto modifiche inadeguate o non corrette possono causare gravi problemi di configurazione nel sistema. La modifica del Registro di sistema tramite l'editor corrispondente deve essere pertanto eseguita esclusivamente da utenti esperti. Per ulteriori informazioni, vedere la documentazione di Microsoft Windows.  
  
### <a name="Security"></a>Sicurezza  
  
#### <a name="Permissions"></a>Autorizzazioni  
È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-specify-a-target-servers-location"></a>Per specificare la posizione di un server di destinazione  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server master in cui si desidera specificare il percorso di un server di destinazione.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, scegliere **Amministrazione multiserver**e selezionare **Gestione server di destinazione**.  
  
3.  Fare clic con il pulsante destro del mouse su un server di destinazione e selezionare **Proprietà**.  
  
4.  Nella casella **Percorso** immettere un percorso per il server e quindi fare clic su **OK**.  
  
## <a name="TsqlProcedure"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-specify-a-target-servers-location"></a>Per specificare la posizione di un server di destinazione  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE msdb ;  
    GO  
    -- enlists the current server into the AdventureWorks1 master server.   
    -- The location for the current server is Building 21, Room 309, Rack 5  
    EXEC dbo.sp_msx_enlist N'AdventureWorks2012',   
        N'Building 21, Room 309, Rack 5' ;  
    GO  
    ```  
  
Per altre informazioni, vedere [sp_msx_enlist (Transact-SQL)](https://msdn.microsoft.com/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f).  
  
