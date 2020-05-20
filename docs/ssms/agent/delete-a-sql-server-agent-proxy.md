---
title: Delete a SQL Server Agent Proxy
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting SQL Server Agent proxies
- proxies [SQL Server Agent], deleting
- removing SQL Server Agent proxies
ms.assetid: 9248841d-7294-47d4-94f3-b34a0521fabc
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6c05f4e2739b2683ecb74a1aa65e98de85e36bb4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246337"
---
# <a name="delete-a-sql-server-agent-proxy"></a>Delete a SQL Server Agent Proxy
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene descritto come eliminare un account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitazioni e restrizioni  
  
-   Quando si elimina un account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, assicurarsi che il proxy non faccia riferimento ad alcun passaggio di processo attivo. Per verificare eventuali passaggi di processo che fanno riferimento al proxy, fare clic con il pulsante destro del mouse sul proxy, scegliere **Proprietà** e nella finestra di dialogo **Proprietà account proxy**_nome\_proxy_ selezionare la pagina **Riferimenti**. Se si elimina un proxy, la finestra di dialogo **Elimina oggetto** consente di riassegnare tutti i passaggi di processo che utilizzano tale proxy.  
  
-   I proxy di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent utilizzano le credenziali per archiviare le informazioni sugli account utente di Windows. L'utente specificato nella credenziale deve disporre dell'autorizzazione "accesso come processo batch" sul computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent verifica l'accesso al sottosistema per un proxy e garantisce l'accesso al proxy ad ogni esecuzione del passaggio di processo. Se il proxy non dispone più di accesso al sottosistema, il passaggio di processo non viene eseguito correttamente. In caso contrario, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent rappresenta l'utente specificato nel proxy ed esegue il passaggio di processo.  
  
-   Se l'account di accesso per l'utente viene utilizzato per l'accesso al proxy oppure se l'utente appartiene a un qualsiasi ruolo che prevede l'accesso al proxy, l'utente potrà utilizzare il proxy in un passaggio di processo.  
  
### <a name="security"></a><a name="Security"></a>Sicurezza  
  
#### <a name="permissions"></a><a name="Permissions"></a>Autorizzazioni  
Gli account proxy possono essere creati, modificati o eliminati unicamente dai membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>Per eliminare un account proxy di SQL Server Agent  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere un server che contiene l'account proxy da eliminare.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic sul segno più per espandere la cartella **Proxy** .  
  
4.  Fare clic sul segno più per espandere il sottosistema che contiene l'account proxy da eliminare, ad esempio **ActiveX Script**.  
  
5.  Fare clic con il pulsante destro del mouse sull'account proxy da eliminare e quindi scegliere **Elimina**.  
  
6.  Nella finestra di dialogo **Elimina oggetto** verificare che sia selezionato l'account proxy corretto. Selezionare la casella di controllo **Riassegna a** per riassegnare i passaggi del processo che si riferiscono all'account proxy a un altro account.  
  
7.  Fare clic su **OK**.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>Per eliminare un account proxy di SQL Server Agent  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- deletes the proxy "Catalog application proxy"  
    USE msdb ;  
    GO  
    EXEC dbo.sp_delete_proxy  
        @proxy_name = N'Catalog application proxy' ;  
    GO  
    ```  
  
Per altre informazioni, vedere [sp_delete_proxy (Transact-SQL)](https://msdn.microsoft.com/44a1db13-b7f2-4dab-a1b5-b8dafb41737c).  
  
