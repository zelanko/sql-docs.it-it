---
title: Modello di sicurezza dell'agente di replica | Microsoft Docs
ms.custom: ''
ms.date: 10/07/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, security
- agents [SQL Server replication], security
- Distribution Agent, security
- logins [SQL Server replication], permissions for agents
- security [SQL Server replication], agent security model
- Log Reader Agent, security
- Queue Reader Agent, security
- Merge Agent, security
- replication [SQL Server], agents and profiles
ms.assetid: 6d09fc8d-843a-4a7a-9812-f093d99d8192
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: da597bf97422f5a0960062b385bc0b67338edfe1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85004959"
---
# <a name="replication-agent-security-model"></a>Modello di sicurezza dell'agente di replica
  Il modello di sicurezza dell'agente di replica consente un controllo accurato degli account utilizzati per l'esecuzione e le connessioni degli agenti. È possibile specificare un account diverso per ogni agente. Per altre informazioni su come specificare gli account, vedere [Gestire gli account di accesso e le password nella replica](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication).  
  
> [!IMPORTANT]  
>  Quando un membro del ruolo predefinito del server **sysadmin** configura la replica, è possibile configurare gli agenti di replica in modo che rappresentino l'account di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent. A tale scopo è necessario non specificare un account di accesso e una password per un agente di replica. Si tratta comunque di un approccio non consigliato. Ai fini della sicurezza, è consigliabile invece specificare un account per ogni agente dotato delle autorizzazioni minime descritte nella sezione "Autorizzazioni richieste per gli agenti" più avanti in questo argomento.  
  
 Gli agenti di replica, come tutti i file eseguibili, vengono eseguiti nel contesto di un account di Windows. Utilizzano tale account per le connessioni con sicurezza integrata di Windows. L'account con il quale viene eseguito l'agente dipende dalla modalità di avvio di quest'ultimo:  
  
-   Avvio dell'agente da un processo predefinito di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent: quando si utilizza un processo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent per avviare un agente di replica, l'agente viene eseguito nel contesto di un account specificato al momento della configurazione della replica. Per ulteriori informazioni su [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent e la replica, vedere la sezione "Sicurezza agente in SQL Server Agent" più avanti in questo argomento. Per altre informazioni sulle autorizzazioni necessarie per l'account usato per l'esecuzione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent, vedere [Configurare SQL Server Agent](../../../ssms/agent/configure-sql-server-agent.md).  
  
-   Avvio dell'agente da una riga dei comandi MS-DOS, direttamente o tramite uno script: l'agente viene eseguito nel contesto dell'account dell'utente che esegue l'agente dalla riga di comando.  
  
-   Avvio dell'agente da un'applicazione che utilizza oggetti RMO (Replication Management Objects) o un controllo ActiveX: l'agente viene eseguito nel contesto dell'applicazione che chiama gli oggetti RMO o il controllo ActiveX.  
  
    > [!NOTE]  
    >  I controlli ActiveX sono deprecati.  
  
 È consigliabile stabilire le connessioni nel contesto della sicurezza integrata di Windows. Per motivi di compatibilità con le versioni precedenti, è anche possibile utilizzare la sicurezza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per ulteriori informazioni sulle procedure consigliate, vedere [Replication Security Best Practices](replication-security-best-practices.md).  
  
## <a name="permissions-that-are-required-by-agents"></a>Autorizzazioni richieste per gli agenti  
 Gli account utilizzati per l'esecuzione e le connessioni degli agenti richiedono varie autorizzazioni. Tali autorizzazioni sono descritte nella tabella seguente. È consigliabile eseguire ogni agente con un account di Windows differente e assegnare all'account solo le autorizzazioni necessarie. Per informazioni sull'elenco di accesso alla pubblicazione, rilevante per numerosi agenti, vedere [Proteggere il server di pubblicazione](secure-the-publisher.md).  
  
> [!NOTE]  
>  Controllo account utente in alcuni sistemi operativi Windows può impedire l'accesso amministrativo alla condivisione snapshot. Le autorizzazioni per la condivisione snapshot devono pertanto essere concesse in modo esplicito agli account di Windows utilizzati dall'agente snapshot, dall'agente di distribuzione e dall'agente di merge. È necessario eseguire questa operazione anche se gli account di Windows sono membri del gruppo Administrators. Per altre informazioni, vedere [proteggere la cartella snapshot](secure-the-snapshot-folder.md).  
  
|Agente|Autorizzazioni|  
|-----------|-----------------|  
|agente snapshot|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al server di distribuzione. Tale account deve:<br /><br /> Come minimo, essere un membro del ruolo predefinito del database **db_owner** nel database di distribuzione.<br /><br /> - Avere le autorizzazioni di lettura, scrittura e modifica per la condivisione snapshot.<br /><br /> <br /><br /> L'account utilizzato per la connessione al server di pubblicazione deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di pubblicazione.|  
|Agente di lettura log|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al server di distribuzione. Tale account deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di distribuzione.<br /><br /> L'account utilizzato per la connessione al server di pubblicazione deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di pubblicazione.<br /><br /> Quando si selezionano le `sync_type` Opzioni *solo supporto replica*, *inizializza con backup*o *Inizializza da LSN*, l'agente di lettura log deve essere eseguito dopo l'esecuzione `sp_addsubscription` di, in modo che gli script di configurazione vengano scritti nel database di distribuzione. L'agente di lettura log deve essere in esecuzione con un account membro del ruolo predefinito del server **sysadmin** . Quando l' `sync_type` opzione è impostata su *automatico*, non sono necessarie azioni speciali dell'agente di lettura log.|  
|Agente di distribuzione per una sottoscrizione push|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al server di distribuzione. Tale account deve:<br /><br /> -Essere almeno un membro del ruolo predefinito del database **db_owner** nel database di distribuzione.<br /><br /> - Essere un membro dell'elenco di accesso alla pubblicazione.<br /><br /> - Avere le autorizzazioni di lettura per la condivisione snapshot.<br /><br /> - Avere le autorizzazioni di lettura per la directory di installazione del provider OLE DB per il Sottoscrittore se la sottoscrizione riguarda un Sottoscrittore non SQL Server.<br /><br /> - Quando si esegue la replica dei dati line-of-business, l'agente di distribuzione deve avere le autorizzazioni di scrittura per la replica **C:\Programmi\Microsoft SQL Server\XX\COMfolder** dove XX rappresenta l'ID istanza.<br /><br /> <br /><br /> L'account utilizzato per la connessione al Sottoscrittore deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione o disporre di autorizzazioni equivalenti se la sottoscrizione riguarda un Sottoscrittore non SQL Server.<br /><br /> Nota: quando si usa nell' `-subscriptionstreams >= 2` agente di distribuzione, è necessario concedere anche l' `View Server State` autorizzazione per i sottoscrittori per rilevare i deadlock.|  
|Agente di distribuzione per una sottoscrizione pull|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al Sottoscrittore. Tale account deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione. L'account utilizzato per la connessione al server di distribuzione deve:<br /><br /> - Essere un membro dell'elenco di accesso alla pubblicazione.<br /><br /> - Avere le autorizzazioni di lettura per la condivisione snapshot.<br /><br /> - Quando si esegue la replica dei dati line-of-business, l'agente di distribuzione deve avere le autorizzazioni di scrittura per la replica **C:\Programmi\Microsoft SQL Server\XX\COMfolder** dove XX rappresenta l'ID istanza.<br /><br /> <br /><br /> Nota: quando si usa nell' `-subscriptionstreams >= 2` agente di distribuzione, è necessario concedere anche l' `View Server State` autorizzazione per i sottoscrittori per rilevare i deadlock.|  
|Agente di merge per una sottoscrizione push|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al server di pubblicazione e al server di distribuzione. Tale account deve:<br /><br /> -Essere almeno un membro del ruolo predefinito del database **db_owner** nel database di distribuzione.<br /><br /> - Essere un membro dell'elenco di accesso alla pubblicazione.<br /><br /> - Essere un account di accesso associato a un utente nel database di pubblicazione.<br /><br /> - Avere le autorizzazioni di lettura per la condivisione snapshot.<br /><br /> <br /><br /> L'account utilizzato per la connessione al Sottoscrittore deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione.|  
|Agente di merge per una sottoscrizione pull|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al Sottoscrittore. Tale account deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione. L'account utilizzato per la connessione al server di pubblicazione e al server di distribuzione deve:<br /><br /> - Essere un membro dell'elenco di accesso alla pubblicazione.<br /><br /> - Essere un account di accesso associato a un utente nel database di pubblicazione.<br /><br /> - Essere un account di accesso associato a un utente nel database di distribuzione. L'utente può essere l'utente `Guest`.<br /><br /> - Avere le autorizzazioni di lettura per la condivisione snapshot.|  
|Agente di lettura coda|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al server di distribuzione. Tale account deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di distribuzione.<br /><br /> L'account utilizzato per la connessione al server di pubblicazione deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di pubblicazione.<br /><br /> L'account utilizzato per la connessione al Sottoscrittore deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione.|  
  
## <a name="agent-security-under-sql-server-agent"></a>Sicurezza agente in SQL Server Agent  
 Quando si configura la replica mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], le procedure [!INCLUDE[tsql](../../../includes/tsql-md.md)] o gli oggetti RMO, per impostazione predefinita viene creato un processo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent per ogni agente. Gli agenti vengono quindi eseguiti nel contesto di un passaggio del processo, indipendentemente dal fatto che l'esecuzione sia continua, in base a una pianificazione o su richiesta. È possibile visualizzare tali processi nella cartella **Processi** in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Nella tabella seguente sono elencati i nomi dei processi.  
  
|Agente|Nome processo|  
|-----------|--------------|  
|agente snapshot|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<integer>**|  
|Agente snapshot per una partizione di una pubblicazione di tipo merge|**Dyn_\<Publisher>-\<PublicationDatabase>-\<Publication>-\<GUID>**|  
|Agente di lettura log|**\<Publisher>-\<PublicationDatabase>-\<integer>**|  
|Agente di merge per le sottoscrizioni pull|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<integer>**|  
|Agente di merge per le sottoscrizioni push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
|Agente di distribuzione per le sottoscrizioni push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**<sup>1</sup>|  
|Agente di distribuzione per le sottoscrizioni pull|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<GUID>**<sup>2</sup>|  
|Agente di distribuzione per le sottoscrizioni push di Sottoscrittori non SQL Server|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
|Agente di lettura coda|**[\<Distributor>].\<integer>**|  
  
 <sup>1</sup> per le sottoscrizioni push di pubblicazioni Oracle, il nome del processo è * * \<Publisher> - \<Publisher**> anziché **\<Publisher>-\<PublicationDatabase>** .  
  
 <sup>2</sup> per le sottoscrizioni pull di pubblicazioni Oracle, il nome del processo è * * \<Publisher> - \<DistributionDatabase**> anziché **\<Publisher>-\<PublicationDatabase>** .  
  
 Durante la configurazione della replica si specificano gli account utilizzati per l'esecuzione degli agenti. Tutti i passaggi del processo, tuttavia, vengono eseguiti nel contesto di sicurezza di un *proxy*e pertanto la replica esegue internamente i mapping seguenti per gli account dell'agente specificati:  
  
-   Prima di tutto viene eseguito il mapping tra l'account e una credenziale usando l'istruzione  [CREATE CREDENTIAL](/sql/t-sql/statements/create-credential-transact-sql) di [!INCLUDE[tsql](../../../includes/tsql-md.md)]. I proxy di[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent utilizzano le credenziali per archiviare le informazioni sugli account utente di Windows.  
  
-   Viene chiamata la stored procedure [sp_add_proxy](/sql/relational-databases/system-stored-procedures/sp-add-proxy-transact-sql) e le credenziali vengono utilizzate per creare un proxy.  
  
> [!NOTE]  
>  Queste informazioni vengono fornite allo scopo di illustrare i processi richiesti per l'esecuzione degli agenti nel contesto di sicurezza appropriato. Non è in genere necessario interagire direttamente con le credenziali o i proxy creati.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure consigliate per la sicurezza della replica](replication-security-best-practices.md)   
 [Sicurezza replica di SQL Server](view-and-modify-replication-security-settings.md)   
 [Proteggere la cartella snapshot](secure-the-snapshot-folder.md)  
  
  
