---
title: Procedura guidata Crea database
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.createdbwiz.f1
ms.assetid: 45fe7a23-a46c-4d40-8bca-3431fbfc5c9d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a5ed33054cc497761775a83eba8d023fe215fcd9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729422"
---
# <a name="create-database-wizard-master-data-services-configuration-manager"></a>Procedura guidata Crea database (Gestione configurazione Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Usare la procedura guidata **Crea database** per creare un database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
## <a name="database-server"></a>Server di database  
 Specificare le informazioni per connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] locale o remota per l'hosting del database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Per connettersi a un'istanza remota, è necessario che questa sia abilitata per le connessioni remote.  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**Istanza di SQL Server**|Specificare il nome dell'istanza del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] in cui si vuole ospitare il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Può corrispondere a un'istanza predefinita o denominata in un computer locale o remoto. Specificare le informazioni digitando quanto segue:<br /><br /> Un punto (.) per connettersi all'istanza predefinita nel computer locale.<br /><br /> Il nome server o l'indirizzo IP per connettersi all'istanza predefinita nel computer locale o remoto specificato.<br /><br /> Il nome server o l'indirizzo IP, nonché il nome dell'istanza per la connessione all'istanza denominata nel computer locale o remoto specificato. Specificare le informazioni nel formato *nome_server*\\*nome_istanza*.|  
|**Tipo di autenticazione**|Selezionare il tipo di autenticazione da utilizzare per la connessione all'istanza di SQL Server specificata. Le credenziali usate per connettersi devono far parte del ruolo del server **sysadmin** per l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] specificata. Per altre informazioni sul ruolo sysadmin, vedere [Ruoli a livello di server](../relational-databases/security/authentication-access/server-level-roles.md).<br /><br /> Nei tipi di autenticazione sono inclusi:<br /><br /> **Utente corrente - Sicurezza integrata**: usa l'autenticazione integrata di Windows per connettersi con le credenziali dell'account utente di Windows corrente. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] usa le credenziali di Windows dell'utente che ha eseguito l'accesso al computer e ha aperto l'applicazione. Non è possibile specificare credenziali di Windows diverse nell'applicazione. Se si desidera connettersi con credenziali di Windows diverse, sarà necessario accedere al computer con il nome utente desiderato, quindi aprire [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].<br /><br /> **Account di SQL Server**: usa un account di SQL Server per la connessione. Quando si seleziona questa opzione, i campi **Nome utente** e **Password** sono abilitati ed è necessario specificare le credenziali per un account di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] specificata.|  
|**User name**|Specificare il nome dell'account utente che verrà usato per connettersi all'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] specificata. L'account deve far parte del ruolo **sysadmin** nell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] specificata.<br /><br /> Quando l'opzione **Tipo di autenticazione** è impostata su **Utente corrente - Sicurezza integrata**, la casella **Nome utente** è di sola lettura e visualizza il nome dell'account utente di Windows usato per l'accesso al computer.<br /><br /> Quando l'opzione **Tipo di autenticazione** è impostata su **Account di SQL Server**, la casella **Nome utente** è abilitata ed è necessario specificare le credenziali per un account di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] specificata.|  
|**Password**|Specificare la password associata all'account utente:<br /><br /> Quando l'opzione **Tipo di autenticazione** è impostata su **Utente corrente - Sicurezza integrata**, la casella **Password** è di sola lettura e per la connessione vengono usate le credenziali dell'account utente di Windows specificato.<br /><br /> Quando l'opzione **Tipo di autenticazione** è impostata su **Account di SQL Server**, la casella **Password** è abilitata ed è necessario specificare la password associata all'account utente specificato.|  
|**Test connessione**|Verificare che l'account utente specificato sia in grado di connettersi all'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e che l'account disponga delle autorizzazioni necessarie per creare un database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] per tale istanza. Se non si fa clic su **Test connessione**, la connessione verrà sottoposta a test quando si fa clic su **Avanti**.|  
  
## <a name="database"></a>database  
 Specificare un nome di database e le opzioni delle regole di confronto per il nuovo database. Le regole di confronto di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] forniscono regole di ordinamento e proprietà di distinzione tra maiuscole e minuscole e tra caratteri accentati e non accentati per i dati. Le regole di confronto utilizzate con dati di tipo carattere, quali char e varchar, definiscono la tabella codici e i caratteri corrispondenti che possono essere rappresentati per quel tipo di dati. Per altre informazioni sulle regole di confronto del database, vedere [Regole di confronto e supporto Unicode](../relational-databases/collations/collation-and-unicode-support.md).  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**Nome database**|Specificare un nome per il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].|  
|**Regole di confronto predefinite di SQL Server**|Selezionare questa opzione per usare l'impostazione delle regole di confronto del database corrente dell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] specificata per il nuovo database.|  
|**Regole di confronto di Windows**|Specificare le impostazioni delle regole di confronto di Windows da utilizzare per il nuovo database. Le regole di confronto di Windows definiscono le regole per l'archiviazione dei dati di tipo carattere in base alle impostazioni locali di Windows associate. Per altre informazioni sulle regole di confronto di Windows e sulle opzioni associate, vedere [Windows_collation_name &#40;Transact-SQL&#41;](../t-sql/statements/windows-collation-name-transact-sql.md).<br /><br /> Nota: l'elenco **Regole di confronto di Windows** e le opzioni associate vengono abilitati solo dopo avere deselezionato la casella **Regole di confronto predefinite di SQL Server**.|  
  
## <a name="administrator-account"></a>Account amministratore  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**User name**|Specificare l'utente con privilegi avanzati predefinito per [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. L'utente con privilegi avanzati ha accesso a tutte le aree funzionali e può aggiungere, eliminare e aggiornare tutti i modelli. Per informazioni sull'autorizzazione dell'utente con privilegi avanzati e sugli altri tipi di amministratori in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).|  
  
## <a name="summary"></a>Riepilogo  
 Consente di visualizzare un riepilogo delle opzioni selezionate. Esaminare le selezioni e quindi fare clic su **Avanti** per iniziare a creare il database con le impostazioni specificate.  
  
## <a name="progress-and-finish"></a>Continua e termina  
 Consente di visualizzare lo stato di avanzamento del processo di creazione. Dopo aver creato il database, fare clic su **Fine** per chiudere la procedura guidata del database e tornare alla pagina **Database**. Il nuovo database risulterà selezionato e sarà possibile visualizzare e modificare le impostazioni di sistema corrispondenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Pagina Configurazione database &#40;Gestione configurazione Master Data Services&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
[Installazione e configurazione di Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md) [Requisiti del database &#40;Master Data Services&#41;](../master-data-services/install-windows/database-requirements-master-data-services.md)  
  
  
