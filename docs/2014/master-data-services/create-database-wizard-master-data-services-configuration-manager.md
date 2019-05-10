---
title: Procedura guidata Crea database (Gestione configurazione Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.createdbwiz.f1
ms.assetid: 45fe7a23-a46c-4d40-8bca-3431fbfc5c9d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7207cd8e3a087ed0aa85931254754d4009d73c53
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479875"
---
# <a name="create-database-wizard-master-data-services-configuration-manager"></a>Procedura guidata Crea database (Gestione configurazione Master Data Services)
  Usare la procedura guidata **Crea database** per creare un database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
## <a name="database-server"></a>Server di database  
 Specificare le informazioni per connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] locale o remota per l'hosting del database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Per connettersi a un'istanza remota, è necessario che questa sia abilitata per le connessioni remote.  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**Istanza di SQL Server**|Specificare il nome dell'istanza del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] in cui si vuole ospitare il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Può corrispondere a un'istanza predefinita o denominata in un computer locale o remoto. Specificare le informazioni digitando quanto segue:<br /><br /> Un punto (.) per connettersi all'istanza predefinita nel computer locale.<br /><br /> Il nome server o l'indirizzo IP per connettersi all'istanza predefinita nel computer locale o remoto specificato.<br /><br /> Il nome server o l'indirizzo IP, nonché il nome dell'istanza per la connessione all'istanza denominata nel computer locale o remoto specificato. Specificare le informazioni nel formato *nome_server*\\*nome_istanza*.|  
|**Tipo di autenticazione**|Selezionare il tipo di autenticazione da utilizzare per la connessione all'istanza di SQL Server specificata. Le credenziali usate per connettersi devono far parte del ruolo del server **sysadmin** per l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] specificata. Per altre informazioni sul ruolo sysadmin, vedere [Ruoli a livello di server](../relational-databases/security/authentication-access/server-level-roles.md). Nei tipi di autenticazione sono inclusi:<br /><br /> **Utente corrente - sicurezza integrata**: usa l'autenticazione integrata di Windows per connettersi con le credenziali dell'account utente di Windows corrente. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] usa le credenziali di Windows dell'utente che ha eseguito l'accesso al computer e ha aperto l'applicazione. Non è possibile specificare credenziali di Windows diverse nell'applicazione. Se si desidera connettersi con credenziali di Windows diverse, sarà necessario accedere al computer con il nome utente desiderato, quindi aprire [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].<br /><br /> **Account di SQL Server**: usa un account di SQL Server per la connessione. Quando si seleziona questa opzione, i campi **Nome utente** e **Password** sono abilitati ed è necessario specificare le credenziali per un account di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] specificata.|  
|**Nome utente**|Specificare il nome dell'account utente che verrà usato per connettersi all'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] specificata. L'account deve far parte del ruolo **sysadmin** nell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] specificata.<br /><br /> Quando l'opzione **Tipo di autenticazione** è impostata su **Utente corrente - Sicurezza integrata**, la casella **Nome utente** è di sola lettura e visualizza il nome dell'account utente di Windows usato per l'accesso al computer.<br /><br /> Quando l'opzione **Tipo di autenticazione** è impostata su **Account di SQL Server**, la casella **Nome utente** è abilitata ed è necessario specificare le credenziali per un account di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] specificata.|  
|**Password**|Specificare la password associata all'account utente.<br /><br /> Quando l'opzione **Tipo di autenticazione** è impostata su **Utente corrente - Sicurezza integrata**, la casella **Password** è di sola lettura e per la connessione vengono usate le credenziali dell'account utente di Windows specificato.<br /><br /> Quando l'opzione **Tipo di autenticazione** è impostata su **Account di SQL Server**, la casella **Password** è abilitata ed è necessario specificare la password associata all'account utente specificato.|  
|**Test connessione**|Verificare che l'account utente specificato sia in grado di connettersi all'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e che l'account disponga delle autorizzazioni necessarie per creare un database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] per tale istanza. Se non si fa clic su **Test connessione**, la connessione verrà sottoposta a test quando si fa clic su **Avanti**.|  
  
## <a name="database"></a>Database  
 Specificare un nome di database e le opzioni delle regole di confronto per il nuovo database. Le regole di confronto di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] forniscono regole di ordinamento e proprietà di distinzione tra maiuscole e minuscole e tra caratteri accentati e non accentati per i dati. Le regole di confronto utilizzate con dati di tipo carattere, quali char e varchar, definiscono la tabella codici e i caratteri corrispondenti che possono essere rappresentati per quel tipo di dati. Per altre informazioni sulle regole di confronto del database, vedere [Regole di confronto e supporto Unicode](../relational-databases/collations/collation-and-unicode-support.md).  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**Nome database**|Specificare un nome per il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**Regole di confronto predefinite di SQL Server**|Selezionare questa opzione per usare l'impostazione delle regole di confronto del database corrente dell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] specificata per il nuovo database.|  
|**Regole di confronto di Windows**|Specificare le impostazioni delle regole di confronto di Windows da utilizzare per il nuovo database. Le regole di confronto di Windows definiscono le regole per l'archiviazione dei dati di tipo carattere in base alle impostazioni locali di Windows associate. Per altre informazioni sulle regole di confronto di Windows e sulle opzioni associate, vedere [Windows_collation_name &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql).<br /><br /> Nota: L'elenco **Regole di confronto di Windows** e le opzioni associate vengono abilitate solo dopo che è stata deselezionata la casella **Regole di confronto predefinite di SQL Server**.|  
  
## <a name="administrator-account"></a>Account amministratore  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**Nome utente**|Specificare un account utente di dominio con ruolo di amministratore di sistema di [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Per tutti i [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] le applicazioni Web associate a questo database, tale utente possono aggiornare tutti i modelli e i dati in tutte le aree funzionali. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).|  
  
## <a name="summary"></a>Riepilogo  
 Consente di visualizzare un riepilogo delle opzioni selezionate. Esaminare le selezioni e quindi fare clic su **Avanti** per iniziare a creare il database con le impostazioni specificate.  
  
## <a name="progress-and-finish"></a>Continua e termina  
 Consente di visualizzare lo stato di avanzamento del processo di creazione. Dopo aver creato il database, fare clic su **Fine** per chiudere la procedura guidata del database e tornare alla pagina **Database** . Il nuovo database risulterà selezionato e sarà possibile visualizzare e modificare le impostazioni di sistema corrispondenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Pagina Configurazione database &#40;Gestione configurazione Master Data Services&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Configurare il Database e il sito Web per Master Data Services](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Requisiti del database &#40;Master Data Services&#41;](install-windows/database-requirements-master-data-services.md)  
  
  
