---
title: Visualizzare o modificare le proprietà del server (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- viewing server properties
- server properties [SQL Server]
- displaying server properties
- servers [SQL Server], viewing
ms.assetid: 55f3ac04-5626-4ad2-96bd-a1f1b079659d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5c5ff985b62e39287b696e96f10142daf90ae0a3
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783130"
---
# <a name="view-or-change-server-properties-sql-server"></a>Visualizzare o modificare le proprietà del server (SQL Server)
  In questo argomento viene illustrato come visualizzare o modificare le proprietà di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o Gestione configurazione SQL Server.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare o modificare le proprietà del server tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Gestione configurazione SQL Server](#PowerShellProcedure)  
  
-   **Completamento:**  [Dopo la modifica delle proprietà del server](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Quando si utilizza sp_configure è necessario eseguire RECONFIGURE oppure RECONFIGURE WITH OVERRIDE dopo aver impostato un'opzione di configurazione. L'istruzione RECONFIGURE WITH OVERRIDE è generalmente riservata alle opzioni di configurazione che dovrebbero essere utilizzate con estrema cautela. È comunque possibile utilizzare l'istruzione RECONFIGURE WITH OVERRIDE con tutte le opzioni di configurazione, anche in sostituzione di RECONFIGURE.  
  
    > [!NOTE]  
    >  L'istruzione RECONFIGURE viene eseguita all'interno di una transazione. Se una delle operazioni di riconfigurazione ha esito negativo, nessuna operazione di riconfigurazione sarà resa effettiva.  
  
-   In alcune pagine delle proprietà sono presenti dati ottenuti tramite il servizio Strumentazione gestione Windows (WMI). Per visualizzare queste pagine, è necessario che nel computer che esegue [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]sia installato il servizio WMI.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per altre informazioni, vedere [Ruoli a livello di Server](../../relational-databases/security/authentication-access/server-level-roles.md).  
  
 Per impostazione predefinita, le autorizzazioni di esecuzione per `sp_configure` senza parametri o solo con il primo parametro vengono concesse a tutti gli utenti. Per eseguire `sp_configure` con entrambi i parametri per modificare un'opzione di configurazione o per eseguire l'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-view-or-change-server-properties"></a>Per visualizzare o modificare le proprietà del server  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo **Proprietà server** fare clic su una pagina per visualizzare o modificare le relative informazioni del server. Alcune proprietà sono di sola lettura.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-view-server-properties-by-using-the-serverproperty-built-in-function"></a>Per visualizzare le proprietà del server tramite la funzione predefinita SERVERPROPERTY  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene usata la funzione predefinita [SERVERPROPERTY](/sql/t-sql/functions/serverproperty-transact-sql) in un'istruzione `SELECT` per restituire informazioni sul server corrente. Ciò risulta utile quando in un server basato su Windows sono installate più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il client deve aprire un'altra connessione alla stessa istanza utilizzata dalla connessione corrente.  
  
    ```sql  
    SELECT CONVERT( sysname, SERVERPROPERTY('servername'));  
    GO  
    ```  
  
#### <a name="to-view-server-properties-by-using-the-sysservers-catalog-view"></a>Per visualizzare le proprietà del server tramite la vista del catalogo sys.servers  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene eseguita una query nella vista del catalogo [sys.servers](/sql/relational-databases/system-catalog-views/sys-servers-transact-sql) per restituire il nome (`name`) e l'ID (`server_id`) del server corrente e il nome del provider OLE DB (`provider`) per la connessione a un server collegato.  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    SELECT name, server_id, provider  
    FROM sys.servers ;   
    GO
    ```  
  
#### <a name="to-view-server-properties-by-using-the-sysconfigurations-catalog-view"></a>Per visualizzare le proprietà del server tramite la vista del catalogo sys.configurations  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene eseguita una query nella vista del catalogo [sys.configurations](/sql/relational-databases/system-catalog-views/sys-configurations-transact-sql) per restituire informazioni su ogni opzione di configurazione del server nel server corrente. Nell'esempio vengono restituiti il nome (`name`) e la descrizione (`description`) dell'opzione e viene indicato se l'opzione è avanzata (`is_advanced`).  
  
    ```sql
    USE AdventureWorks2012;
    GO  
    SELECT name, description, is_advanced  
    FROM sys.configurations ;
    GO
    ```  
  
#### <a name="to-change-a-server-property-by-using-sp_configure"></a>Per modificare una proprietà del server tramite sp_configure  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene illustrato come usare [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) per modificare una proprietà del server. Nell'esempio il valore dell'opzione `fill factor` viene modificato in `100`. Per rendere effettiva la modifica, è necessario riavviare il server.  
  
```sql  
Use AdventureWorks2012;  
GO  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'fill factor', 100;  
GO  
RECONFIGURE;  
GO  
```  
  
 Per altre informazioni, vedere [Server Configuration Options &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
 È possibile visualizzare o modificare alcune proprietà del server tramite Gestione configurazione SQL Server. Ad esempio, è possibile visualizzare la versione e l'edizione dell'istanza di SQL Server o modificare il percorso in cui sono archiviati i file di log degli errori. È inoltre possibile visualizzare queste proprietà eseguendo query nelle [Funzioni a gestione dinamica e DMV correlate al server](/sql/relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql).  
  
#### <a name="to-view-or-change-server-properties"></a>Per visualizzare o modificare le proprietà del server  
  
1.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Strumenti di configurazione**e quindi **Gestione configurazione SQL Server**.  
  
2.  In **Gestione configurazione SQL Server**fare clic su **Servizi di SQL Server**.  
  
3.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **SQL Server (\<***nomeistanza***>)** e scegliere **Proprietà**.  
  
4.  Nella finestra di dialogo **SQL Server (\<***nomeistanza***>) Proprietà** modificare le proprietà del server nella scheda **Servizio** o **Avanzate** e fare clic su **OK**.  
  
##  <a name="FollowUp"></a> Completamento: Dopo la modifica delle proprietà del server  
 Per alcune proprietà, potrebbe essere necessario riavviare il server per rendere effettiva la modifica.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [Istruzioni SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statements-transact-sql)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [Configurazione di WMI per mostrare lo stato del server in Strumenti SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)   
 [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md)   
 [Funzioni di configurazione &#40;Transact-SQL&#41;](/sql/t-sql/functions/configuration-functions-transact-sql)   
 [Funzioni a gestione dinamica e DMV correlate al server &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql)  
