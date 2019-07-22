---
title: Visualizzare o modificare le proprietà del server (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.connectionproperties.f1
helpviewer_keywords:
- viewing server properties
- server properties [SQL Server]
- displaying server properties
- servers [SQL Server], viewing
- Connection Properties dialog box
ms.assetid: 55f3ac04-5626-4ad2-96bd-a1f1b079659d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a604ee89ed33f30d15e5402cba8d04668c7528f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945763"
---
# <a name="view-or-change-server-properties-sql-server"></a>Visualizzare o modificare le proprietà del server (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene illustrato come visualizzare o modificare le proprietà di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o Gestione configurazione SQL Server.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Security](#Security)  
  
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
  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-or-change-server-properties"></a>Per visualizzare o modificare le proprietà del server  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server, quindi scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo **Proprietà server** fare clic su una pagina per visualizzare o modificare le relative informazioni del server. Alcune proprietà sono di sola lettura.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-view-server-properties-by-using-the-serverproperty-built-in-function"></a>Per visualizzare le proprietà del server tramite la funzione predefinita SERVERPROPERTY  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene usata la funzione predefinita [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md) in un'istruzione `SELECT` per restituire informazioni sul server corrente. Ciò risulta utile quando in un server basato su Windows sono installate più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il client deve aprire un'altra connessione alla stessa istanza utilizzata dalla connessione corrente.  
  
    ```sql  
    SELECT CONVERT( sysname, SERVERPROPERTY('servername'));  
    GO  
    ```  
  
#### <a name="to-view-server-properties-by-using-the-sysservers-catalog-view"></a>Per visualizzare le proprietà del server tramite la vista del catalogo sys.servers  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene eseguita una query nella vista del catalogo [sys.servers](../../relational-databases/system-catalog-views/sys-servers-transact-sql.md) per restituire il nome (`name`) e l'ID (`server_id`) del server corrente e il nome del provider OLE DB (`provider`) per la connessione a un server collegato.  
  
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
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene eseguita una query nella vista del catalogo [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) per restituire informazioni su ogni opzione di configurazione del server nel server corrente. Nell'esempio vengono restituiti il nome (`name`) e la descrizione (`description`) dell'opzione e viene indicato se l'opzione è avanzata (`is_advanced`).  
  
    ```wmimof  
    USE AdventureWorks2012;   
    GO  
    SELECT name, description, is_advanced  
    FROM sys.configurations ;   
    GO  
  
    ```  
  
#### <a name="to-change-a-server-property-by-using-spconfigure"></a>Per modificare una proprietà del server tramite sp_configure  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene illustrato come usare [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) per modificare una proprietà del server. Nell'esempio il valore dell'opzione `fill factor` viene modificato in `100`. Per rendere effettiva la modifica, è necessario riavviare il server.  
  
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
  
 Per altre informazioni, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)sia installato il servizio WMI.  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
 È possibile visualizzare o modificare alcune proprietà del server tramite Gestione configurazione SQL Server. Ad esempio, è possibile visualizzare la versione e l'edizione dell'istanza di SQL Server o modificare il percorso in cui sono archiviati i file di log degli errori. È inoltre possibile visualizzare queste proprietà eseguendo query nelle [Funzioni a gestione dinamica e DMV correlate al server](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md).  
  
#### <a name="to-view-or-change-server-properties"></a>Per visualizzare o modificare le proprietà del server  
  
1.  Fare clic sul menu **Start** , scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Strumenti di configurazione**e quindi **Gestione configurazione SQL Server**.  
  
2.  In **Gestione configurazione SQL Server**fare clic su **Servizi di SQL Server**.  
  
3.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **SQL Server (\<** _nomeistanza_ **>)** e quindi scegliere **Proprietà**.  
  
4.  Nella finestra di dialogo **SQL Server (\<** _nomeistanza_ **>) Proprietà** modificare le proprietà del server nella scheda **Servizio** o **Avanzate** e quindi fare clic su **OK**.  
  
##  <a name="FollowUp"></a> Completamento: Dopo la modifica delle proprietà del server  
 Per alcune proprietà, potrebbe essere necessario riavviare il server per rendere effettiva la modifica.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Istruzioni SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Configurare WMI per mostrare lo stato del server in Strumenti SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)   
 [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md)   
 [Funzioni di configurazione &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Funzioni a gestione dinamica e DMV correlate al server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
