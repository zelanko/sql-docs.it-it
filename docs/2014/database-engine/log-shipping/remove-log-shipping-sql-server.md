---
title: Disattivare il log shipping [SQL Server] | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], removing
- removing log shipping
- deleting log shipping
ms.assetid: 859373db-c744-4a4b-8479-45163f61e8cb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 270ca92b723aa67938dc1f56d72425d7e1c98040
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62774995"
---
# <a name="remove-log-shipping-sql-server"></a>Disattivare il log shipping [SQL Server]
  In questo argomento viene descritto come rimuovere il log shipping in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per rimuovere il log shipping utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le stored procedure per il log shipping richiedono l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-remove-log-shipping"></a>Per rimuovere il log shipping  
  
1.  Connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che rappresenta attualmente il server primario di log shipping ed espandere l'istanza.  
  
2.  Espandere **Database**, fare clic con il pulsante destro del mouse sul database primario per il log shipping, quindi scegliere **Proprietà**.  
  
3.  Nella casella **Selezionare una pagina**fare clic su **Log shipping delle transazioni**.  
  
4.  Deselezionare la casella di controllo **Abilita come database primario in una configurazione per il log shipping** .  
  
5.  Fare clic su **OK** per rimuovere il log shipping dal database primario.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-remove-log-shipping"></a>Per rimuovere il log shipping  
  
1.  Nel server primario di log shipping eseguire [sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql) per eliminare le informazioni relative al database secondario.  
  
2.  Nel server secondario di log shipping eseguire [sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql) per eliminare il database secondario.  
  
    > [!NOTE]  
    >  Se non sono disponibili altri database secondari con lo stesso ID secondario, **sp_delete_log_shipping_secondary_primary** viene richiamata da **sp_delete_log_shipping_secondary_database** e tramite essa vengono eliminati la voce relativa all'ID secondario e i processi di copia e ripristino.  
  
3.  Nel server primario di log shipping eseguire **sp_delete_log_shipping_primary_database** per eliminare le informazioni relative alla configurazione per il log shipping. In questo modo verrà eliminato anche il processo di backup.  
  
4.  Nel server primario di log shipping disabilitare il processo di backup. Per altre informazioni, vedere [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md).  
  
5.  Nel server secondario di log shipping disabilitare i processi di copia e ripristino.  
  
6.  Facoltativamente, se non si utilizza più un database secondario per il log shipping, è possibile eliminarlo dal server secondario.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Aggiornare il log shipping a SQL Server 2014 &#40;Transact-SQL&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Configurare il log shipping &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)  
  
-   [Aggiungere un database secondario a una configurazione per il log shipping &#40;SQL Server&#41;](add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [Rimuovere un database secondario da una configurazione per il log shipping &#40;SQL Server&#41;](remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [Monitorare il log shipping &#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
-   [Failover su un database secondario per il log shipping &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul log shipping &#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [Tabelle e stored procedure relative al log shipping](log-shipping-tables-and-stored-procedures.md)  
  
  
