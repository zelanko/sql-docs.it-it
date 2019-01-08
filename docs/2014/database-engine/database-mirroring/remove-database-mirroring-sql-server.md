---
title: Rimuovere il mirroring del database (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], removing
- removing database mirroring [SQL Server]
ms.assetid: bbc4d7f7-3bc7-40d6-a822-af195fe7f8c0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a6d398c2c9d8439025c7ff5ec7a8e4295b24d337
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506130"
---
# <a name="remove-database-mirroring-sql-server"></a>Rimuovere il mirroring del database (SQL Server)
  In questo argomento verrà descritto come rimuovere il mirroring del database da un database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  Il proprietario del database può arrestare manualmente una sessione di mirroring del database in qualsiasi momento, rimuovendo il mirroring dal database.  
  
 
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È richiesta l'autorizzazione ALTER per il database.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-remove-database-mirroring"></a>Per rimuovere il mirroring del database  
  
1.  Durante una sessione di mirroring del database, connettersi all'istanza del server principale e in Esplora oggetti fare clic sul nome del server per espanderne l'albero.  
  
2.  Espandere **Database**e selezionare il database.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **Attività**e quindi fare clic su **Server mirror**. Viene visualizzata la pagina **Mirroring** della finestra di dialogo **Proprietà database** .  
  
4.  Nel riquadro **Selezione pagina** fare clic su **Mirroring**.  
  
5.  Per rimuovere il mirroring, scegliere **Rimuovi mirroring**. Verrà richiesta una conferma. Se si fa clic su **Sì**, la sessione verrà arrestata e il mirroring verrà rimosso dal database.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 Per rimuovere il mirroring del database, utilizzare **Proprietà database**. Utilizzare la pagina **Mirroring** della finestra di dialogo **Proprietà database** .  
  
#### <a name="to-remove-database-mirroring"></a>Per rimuovere il mirroring del database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)] di qualsiasi partner di mirroring.  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Eseguire l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] riportata di seguito.  
  
    ```  
    ALTER DATABASE database_name SET PARTNER OFF  
    ```  
  
     dove *database_name* è il database con mirroring di cui si vuole rimuovere la sessione.  
  
     Nell'esempio seguente viene rimosso il mirroring del database dal database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER OFF;  
    ```  
  
##  <a name="FollowUp"></a> Completamento: Rimozione del mirroring del database  
  
> [!NOTE]  
>  Per informazioni sull'impatto della rimozione del mirroring del database, vedere [Rimozione del mirroring del database &#40;SQL Server&#41;](database-mirroring-sql-server.md).  
  
-   **In caso di riavvio del mirroring nel database**  
  
     Prima di poter riavviare il mirroring è necessario che tutti i backup di log eseguiti nel database principale dopo la rimozione del mirroring vengano applicati al database mirror.  
  
-   **In caso di non riavvio del mirroring**  
  
     Facoltativamente, è possibile recuperare il database mirror precedente. Nell'istanza del server mirror è possibile utilizzare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente:  
  
    ```  
    RESTORE DATABASE database_name WITH RECOVERY;  
    ```  
  
    > [!IMPORTANT]  
    >  Se questo database viene recuperato, online saranno disponibili due database divergenti con lo stesso nome. Di conseguenza, è necessario assicurarsi che i client possano accedere soltanto a uno di essi, generalmente al database principale più recente.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Sospendere o riprendere una sessione di mirroring del database &#40;SQL Server&#41;](pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
-   [Rimuovere il server di controllo del mirroring da una sessione di mirroring del database &#40;SQL Server&#41;](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
-   [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)  
  
-   [Esempio: Configurare tramite certificati di mirroring del Database &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Mirroring del database &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Impostazione del mirroring del database &#40;SQL Server&#41;](setting-up-database-mirroring-sql-server.md)   
 [Gruppi di disponibilità AlwaysOn (SQL Server)](../availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
