---
title: Configure a User to Create and Manage SQL Server Agent Jobs
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6c492a7875eed70cc58efa2dcae8ac180229e5ad
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246502"
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>Configure a User to Create and Manage SQL Server Agent Jobs
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Questo argomento descrive come configurare un utente per la creazione o l'esecuzione di processi di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   **Prima di iniziare:**  [Sicurezza](#Security)  
  
-   **Per configurare un utente per la creazione e la gestione di processi di SQL Server Agent usando:**  [SQL Server Management Studio](#SSMS)  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="security"></a><a name="Security"></a>Sicurezza  
Per configurare un utente per la creazione o l'esecuzione di processi di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, è prima necessario aggiungere un account di accesso esistente di SQL Server o un ruolo msdb a uno dei ruoli predefiniti del database seguenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nel database msdb: SQLAgentUserRole, SQLAgentReaderRole o SQLAgentOperatorRole.  
  
Per impostazione predefinita, i membri di questi ruoli del database possono creare passaggi di processo personalizzati ed eseguirli con il proprio account. Per eseguire processi che includono altri tipi di passaggi, ad esempio pacchetti [!INCLUDE[ssIS](../../includes/ssis_md.md)] , questi utenti non amministrativi dovranno avere accesso a un account proxy. Tutti i membri del ruolo predefinito del server sysadmin dispongono dell'autorizzazione per la creazione, la modifica e l'eliminazione degli account proxy. Per altre informazioni sulle autorizzazioni associate con questi ruoli di database predefiniti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
#### <a name="permissions"></a><a name="Permissions"></a>Autorizzazioni  
Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>Utilizzo di SQL Server Management Studio  
**Per aggiungere un account di accesso SQL o un ruolo msdb a un ruolo predefinito del database di SQL Server Agent**  
  
1.  Espandere un server in **Esplora oggetti**.  
  
2.  Espandere **Sicurezza**e quindi **Account di accesso**.  
  
3.  Fare clic con il pulsante destro del mouse sull'account di accesso che si vuole aggiungere al ruolo predefinito del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e scegliere **Proprietà**.  
  
4.  Nella pagina **Mapping utenti** della finestra di dialogo **Proprietà account di accesso** selezionare la riga contenente **msdb**.  
  
5.  Nell'area **Appartenenza a ruoli del database per: msdb**selezionare il ruolo predefinito del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
**Per configurare un account proxy per la creazione e la gestione dei passaggi di processo di SQL Server Agent**  
  
1.  Espandere un server in **Esplora oggetti**.  
  
2.  Espandere **SQL Server Agent**.  
  
3.  Fare clic con il pulsante destro del mouse su **Proxy** e scegliere **Nuovo proxy**.  
  
4.  Nella pagina **Generale** della finestra **Nuovo account proxy** specificare il nome del proxy, il nome delle credenziali e la descrizione per il nuovo proxy. Si noti che prima di creare un proxy di SQL Server Agent, è necessario innanzitutto creare le credenziali. Per altre informazioni sulla creazione delle credenziali, vedere [Procedura: Creare una credenziale](https://msdn.microsoft.com/c1e77e91-2a69-40d9-b8b3-97cffc710586) e [CREATE CREDENTIAL (Transact-SQL)](https://msdn.microsoft.com/d5e9ae69-41d9-4e46-b13d-404b88a32d9d).  
  
5.  Selezionare i sottosistemi appropriati per il proxy.  
  
6.  Nella pagina **Entità** aggiungere o rimuovere account di accesso oppure ruoli per concedere o negare l'accesso all'account proxy.  
  
## <a name="see-also"></a>Vedere anche  
[Implementazione della sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)  
  
