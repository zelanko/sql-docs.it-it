---
title: Configurare SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, configuring
- accounts [SQL Server], SQL Server Agent
- SQL Server Agent, permissions
- security [SQL Server], SQL Server Agent
ms.assetid: 2e361a62-9e92-4fcd-80d7-d6960f127900
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4f864a063feeaaefccebf384e5ab4725f354fa54
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65100288"
---
# <a name="configure-sql-server-agent"></a>Configurazione di SQL Server Agent
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene descritto come specificare alcune opzioni di configurazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il set completo di opzioni di configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è disponibile solo in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) o nelle stored procedure di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
**Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
    [Limitazioni e restrizioni](#Restrictions)  
  
    [Security](#Security)  
  
-   [Per configurare SQL Server Agent](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Restrictions"></a>Limitazioni e restrizioni  
  
-   Fare clic su **SQL Server Agent** in Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per gestire processi, operatori, avvisi e il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Tuttavia, in Esplora oggetti viene visualizzato il nodo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent solo se si dispone dell'autorizzazione a utilizzarlo.  
  
-   Non è possibile abilitare il riavvio automatico per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nelle istanze del cluster di failover.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
Per la corretta esecuzione delle funzioni, è necessario che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia configurato per utilizzare le credenziali di un account membro del ruolo predefinito del server **sysadmin** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'account deve disporre delle autorizzazioni di Windows seguenti:  
  
-   Accesso come servizio (SeServiceLogonRight)  
  
-   Sostituzione di token a livello di processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorare controllo incrociato (SeChangeNotifyPrivilege)  
  
-   Regolazione quote di memoria per un processo (SeIncreaseQuotaPrivilege)  
  
Per altre informazioni sulle autorizzazioni di Windows necessarie per l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere [Selezionare un account per il servizio SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) e [Impostazione di account di servizio Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-sql-server-agent"></a>Per configurare SQL Server Agent  
  
1.  Fare clic sul pulsante **Start** e scegliere **Pannello di controllo**  dal menu **Start**.  
  
2.  Nel Pannello di controllo fare clic su **Sistema e sicurezza**, scegliere **Strumenti di amministrazione**, quindi **Criteri di sicurezza locali**.  
  
3.  In Criteri di sicurezza locale fare clic sulle virgolette per espandere la cartella **Criteri locali** , quindi scegliere la cartella **Assegnazione diritti utente** .  
  
4.  Fare clic con il pulsante destro del mouse su un'autorizzazione da configurare per l'uso con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e selezionare **Proprietà**.  
  
5.  Nella finestra di dialogo delle proprietà dell'autorizzazione, verificare che sia elencato l'account con cui viene eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. In caso contrario, fare clic su **Aggiungi utente o gruppo**, immettere l'account con cui viene eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nella finestra di dialogo **Selezione utenti, computer, account del servizio o gruppi** , quindi fare clic su **OK**.  
  
6.  Ripetere per ogni autorizzazione da aggiungere per l'esecuzione con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Al termine, fare clic su **OK**.  
  
