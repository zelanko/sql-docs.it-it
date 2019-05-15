---
title: Impostare un alias SQL Server per il servizio SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ae6b9600ec2fb41439d30ece3a8c2fe8bc08008e
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65103227"
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set a SQL Server Alias for the SQL Server Agent Service (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene descritto come impostare un alias [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, da utilizzare per la connessione al [!INCLUDE[ssDE](../../includes/ssde_md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per impostazione predefinita, il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent si connette a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante named pipe utilizzando nomi di server dinamici che non richiedono alcuna configurazione client aggiuntiva. La configurazione di un alias di connessione del server è necessaria solo se non si utilizza il trasporto di rete predefinito o se ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che rimane in attesa su un'altra named pipe.  
  
**Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
    [Limitazioni e restrizioni](#Restrictions)  
  
    [Security](#Security)  
  
-   [Per impostare un alias SQL Server per il servizio SQL Server Agent utilizzando SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Restrictions"></a>Limitazioni e restrizioni  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non funzionerà correttamente se non si seleziona un alias che fa riferimento all'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   In Esplora oggetti viene visualizzato il nodo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent solo se si dispone dell'autorizzazione per utilizzarlo.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
Per la corretta esecuzione delle funzioni, è necessario che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia configurato per utilizzare le credenziali di un account membro del ruolo predefinito del server **sysadmin** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'account deve disporre delle autorizzazioni di Windows seguenti:  
  
-   Accesso come servizio (SeServiceLogonRight)  
  
-   Sostituzione di token a livello di processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorare controllo incrociato (SeChangeNotifyPrivilege)  
  
-   Regolazione quote di memoria per un processo (SeIncreaseQuotaPrivilege)  
  
Per altre informazioni sulle autorizzazioni di Windows necessarie per l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere [Selezionare un account per il servizio SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) e [Impostazione di account di servizio Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>Per impostare un alias SQL Server per il servizio SQL Server Agent  
  
1.  In **Esplora oggetti**connettersi a un'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] e quindi espandere tale istanza.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, quindi scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà SQL Server Agent**_nome\_server_ in **Seleziona una pagina** selezionare **Connessione** e  
  
4.  Nella casella **Alias server host locale** , digitare l'alias del server a cui si deve connettere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
5.  Fare clic su **OK**.  
  
