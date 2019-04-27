---
title: Visualizzare o configurare le opzioni di connessione al server remoto (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- remote servers [SQL Server], connection options
- servers [SQL Server], remote
- connections [SQL Server], remote servers
ms.assetid: 356d3e6b-8514-4bd2-a683-9de147949b2b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5dfc0aa145f106fc57c25a6249b928ee27ab4b87
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757199"
---
# <a name="view-or-configure-remote-server-connection-options-sql-server"></a>Visualizzazione o configurare le opzioni di connessione al server remoto (SQL Server)
  In questo argomento viene descritto come visualizzare e configurare a livello di server le opzioni di connessione al server remoto in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzazione o configurazione le opzioni di connessione al server remoto utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [dopo la configurazione delle opzioni di connessione al server remoto](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 L'esecuzione di **sp_serveroption** richiede l'autorizzazione ALTER ANY LINKED SERVER nel server.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-or-configure-remote-server-connection-options"></a>Per visualizzare o configurare le opzioni di connessione al server remoto  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server, quindi scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo **Proprietà SQL Server - \<***nome_server***>** fare clic su **Connessioni**.  
  
3.  Nella pagina **Connessioni** esaminare le impostazioni relative a **Connessioni remote** e, se necessario, modificarle.  
  
4.  Ripetere i passaggi da 1 a 3 nell'altro server della coppia di server remoti.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-view-remote-server-connection-options"></a>Per visualizzare le opzioni di connessione al server remoto  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene usato [sp_helpserver](/sql/relational-databases/system-stored-procedures/sp-helpserver-transact-sql) per restituire le informazioni su tutti i server remoti.  
  
```sql  
USE master;  
GO  
EXEC sp_helpserver ;  
```  
  
#### <a name="to-configure-remote-server-connection-options"></a>Per configurare le opzioni di connessione al server remoto  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene illustrato come usare [sp_serveroption](/sql/relational-databases/system-stored-procedures/sp-serveroption-transact-sql) per configurare un server remoto. Nell'esempio viene configurata la compatibilità delle regole di confronto tra un server remoto corrispondente a un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `SEATTLE3`e l'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
##  <a name="FollowUp"></a> Completamento: dopo la configurazione delle opzioni di connessione al server remoto  
 Per poter rendere effettiva l'impostazione, è necessario arrestare e riavviare il server remoto.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [Server remoti](remote-servers.md)   
 [Server collegati &#40;Motore di database&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-linkedservers-transact-sql)   
 [sp_helpserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpserver-transact-sql)   
 [sp_serveroption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-serveroption-transact-sql)  
  
  
