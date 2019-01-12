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
manager: craigg
ms.openlocfilehash: 4b919289d49901f64b26db0aa2d4b71eeb0e132a
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133571"
---
# <a name="replication-agent-security-model"></a>Modello di sicurezza dell'agente di replica
  Il modello di sicurezza dell'agente di replica consente un controllo accurato gli account con cui gli agenti di replica eseguire e stabiliscono connessioni: Per ogni agente, è possibile specificare un account diverso. Per altre informazioni su come specificare gli account, vedere [Gestire gli account di accesso e le password nella replica](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication).  
  
> [!IMPORTANT]  
>  Quando un membro del ruolo predefinito del server **sysadmin** configura la replica, è possibile configurare gli agenti di replica in modo che rappresentino l'account di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent. A tale scopo è necessario non specificare un account di accesso e una password per un agente di replica. Si tratta comunque di un approccio non consigliato. Ai fini della sicurezza, è consigliabile invece specificare un account per ogni agente dotato delle autorizzazioni minime descritte nella sezione "Autorizzazioni richieste per gli agenti" più avanti in questo argomento.  
  
 Gli agenti di replica, come tutti i file eseguibili, vengono eseguiti nel contesto di un account di Windows. Utilizzano tale account per le connessioni con sicurezza integrata di Windows. L'account con il quale viene eseguito l'agente dipende dalla modalità di avvio di quest'ultimo:  
  
-   Avvio dell'agente da un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] processo dell'agente, il valore predefinito: Quando un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] processo dell'agente utilizzato per avviare un agente di replica, l'agente viene eseguito nel contesto di un account di specificare quando si configura la replica. Per ulteriori informazioni su [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent e la replica, vedere la sezione "Sicurezza agente in SQL Server Agent" più avanti in questo argomento. Per altre informazioni sulle autorizzazioni necessarie per l'account usato per l'esecuzione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent, vedere [Configurare SQL Server Agent](../../../ssms/agent/configure-sql-server-agent.md).  
  
-   Avvio dell'agente dalla riga di comando MS-DOS, direttamente o tramite uno script: L'agente viene eseguito nel contesto dell'account dell'utente che esegue l'agente dalla riga di comando.  
  
-   Avvio dell'agente da un'applicazione che usa gli oggetti RMO (Replication Management Objects) o un controllo ActiveX: L'agente viene eseguito nel contesto dell'applicazione che chiama gli oggetti RMO o il controllo ActiveX.  
  
    > [!NOTE]  
    >  I controlli ActiveX sono deprecati.  
  
 È consigliabile stabilire le connessioni nel contesto della sicurezza integrata di Windows. Per motivi di compatibilità con le versioni precedenti, è anche possibile utilizzare la sicurezza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per ulteriori informazioni sulle procedure consigliate, vedere [Replication Security Best Practices](replication-security-best-practices.md).  
  
## <a name="permissions-that-are-required-by-agents"></a>Autorizzazioni richieste per gli agenti  
 Gli account utilizzati per l'esecuzione e le connessioni degli agenti richiedono varie autorizzazioni. Tali autorizzazioni sono descritte nella tabella seguente. È consigliabile eseguire ogni agente con un account di Windows differente e assegnare all'account solo le autorizzazioni necessarie. Per informazioni sull'elenco di accesso alla pubblicazione, rilevante per numerosi agenti, vedere [Proteggere il server di pubblicazione](secure-the-publisher.md).  
  
> [!NOTE]  
>  Controllo account utente in alcuni sistemi operativi Windows può impedire l'accesso amministrativo alla condivisione snapshot. Le autorizzazioni per la condivisione snapshot devono pertanto essere concesse in modo esplicito agli account di Windows utilizzati dall'agente snapshot, dall'agente di distribuzione e dall'agente di merge. È necessario eseguire questa operazione anche se gli account di Windows sono membri del gruppo Administrators. Per altre informazioni, vedere [Proteggere la cartella snapshot](secure-the-snapshot-folder.md).  
  
|Agent|Permissions|  
|-----------|-----------------|  
|agente snapshot|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al server di distribuzione. Tale account deve:<br /><br /> - Essere almeno un membro del ruolo predefinito del database **db_owner** nel database di distribuzione.<br /><br /> - Avere le autorizzazioni di lettura, scrittura e modifica per la condivisione snapshot.<br /><br /> <br /><br /> L'account utilizzato per la connessione al server di pubblicazione deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di pubblicazione.|  
|Agente di lettura log|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al server di distribuzione. Tale account deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di distribuzione.<br /><br /> L'account utilizzato per la connessione al server di pubblicazione deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di pubblicazione.<br /><br /> Quando si seleziona il `sync_type` opzioni *solo supporto replica*, *inizializzazione con backup*, o *Inizializza da lsn*, è necessario eseguire l'agente di lettura log dopo l'esecuzione `sp_addsubscription`, in modo che gli script impostati vengano scritti nel database di distribuzione. L'agente di lettura log deve essere in esecuzione con un account membro del ruolo predefinito del server **sysadmin** . Quando la `sync_type` opzione è impostata su *automatica*, è necessaria alcuna azione di agente lettura log speciali.|  
|Agente di distribuzione per una sottoscrizione push|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al server di distribuzione. Tale account deve:<br /><br /> - Essere almeno un membro del ruolo predefinito del database **db_owner** nel database di distribuzione.<br /><br /> - Essere un membro dell'elenco di accesso alla pubblicazione.<br /><br /> - Avere le autorizzazioni di lettura per la condivisione snapshot.<br /><br /> - Avere le autorizzazioni di lettura per la directory di installazione del provider OLE DB per il Sottoscrittore se la sottoscrizione riguarda un Sottoscrittore non SQL Server.<br /><br /> - Quando si esegue la replica dei dati line-of-business, l'agente di distribuzione deve avere le autorizzazioni di scrittura per la replica **C:\Programmi\Microsoft SQL Server\XX\COMfolder** dove XX rappresenta l'ID istanza.<br /><br /> <br /><br /> L'account utilizzato per la connessione al Sottoscrittore deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione o disporre di autorizzazioni equivalenti se la sottoscrizione riguarda un Sottoscrittore non SQL Server.<br /><br /> Nota: Quando si usa `-subscriptionstreams >= 2` sull'agente di distribuzione è necessario concedere anche il `View Server State` per i sottoscrittori per rilevare i deadlock.|  
|Agente di distribuzione per una sottoscrizione pull|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al Sottoscrittore. Tale account deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione. L'account utilizzato per la connessione al server di distribuzione deve:<br /><br /> - Essere un membro dell'elenco di accesso alla pubblicazione.<br /><br /> - Avere le autorizzazioni di lettura per la condivisione snapshot.<br /><br /> - Quando si esegue la replica dei dati line-of-business, l'agente di distribuzione deve avere le autorizzazioni di scrittura per la replica **C:\Programmi\Microsoft SQL Server\XX\COMfolder** dove XX rappresenta l'ID istanza.<br /><br /> <br /><br /> Nota: Quando si usa `-subscriptionstreams >= 2` sull'agente di distribuzione è necessario concedere anche il `View Server State` per i sottoscrittori per rilevare i deadlock.|  
|Agente di merge per una sottoscrizione push|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al server di pubblicazione e al server di distribuzione. Tale account deve:<br /><br /> - Essere almeno un membro del ruolo predefinito del database **db_owner** nel database di distribuzione.<br /><br /> - Essere un membro dell'elenco di accesso alla pubblicazione.<br /><br /> - Essere un account di accesso associato a un utente nel database di pubblicazione.<br /><br /> - Avere le autorizzazioni di lettura per la condivisione snapshot.<br /><br /> <br /><br /> L'account utilizzato per la connessione al Sottoscrittore deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione.|  
|Agente di merge per una sottoscrizione pull|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al Sottoscrittore. Tale account deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione. L'account utilizzato per la connessione al server di pubblicazione e al server di distribuzione deve:<br /><br /> - Essere un membro dell'elenco di accesso alla pubblicazione.<br /><br /> - Essere un account di accesso associato a un utente nel database di pubblicazione.<br /><br /> - Essere un account di accesso associato a un utente nel database di distribuzione. L'utente può essere l'utente `Guest`.<br /><br /> - Avere le autorizzazioni di lettura per la condivisione snapshot.|  
|Agente di lettura coda|L'account di Windows con cui viene eseguito l'agente viene utilizzato per le connessioni al server di distribuzione. Tale account deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di distribuzione.<br /><br /> L'account utilizzato per la connessione al server di pubblicazione deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di pubblicazione.<br /><br /> L'account utilizzato per la connessione al Sottoscrittore deve essere almeno membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione.|  
  
## <a name="agent-security-under-sql-server-agent"></a>Sicurezza agente in SQL Server Agent  
 Quando si configura la replica mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], le procedure [!INCLUDE[tsql](../../../includes/tsql-md.md)] o gli oggetti RMO, per impostazione predefinita viene creato un processo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent per ogni agente. Gli agenti vengono quindi eseguiti nel contesto di un passaggio del processo, indipendentemente dal fatto che l'esecuzione sia continua, in base a una pianificazione o su richiesta. È possibile visualizzare tali processi nella cartella **Processi** in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Nella tabella seguente sono elencati i nomi dei processi.  
  
|Agent|Nome processo|  
|-----------|--------------|  
|agente snapshot|**\<ServerPubblicazione>-\<DatabasePubblicazione>-\<ServerPubblicazione>-\<intero>**|  
|Agente snapshot per una partizione di una pubblicazione di tipo merge|**Dyn_\<ServerPubblicazione>-\<DatabasePubblicazione>-\<Pubblicazione>-\<GUID>**|  
|Agente di lettura log|**\<ServerPubblicazione>-\<DatabasePubblicazione>-\<intero>**|  
|Agente di merge per le sottoscrizioni pull|**\<ServerPubblicazione>-\<DatabasePubblicazione>-\<Pubblicazione>-\<Sottoscrittore>-\<DatabaseSottoscrizione>-\<intero>**|  
|Agente di merge per le sottoscrizioni push|**\<ServerPubblicazione>-\<DatabasePubblicazione>-\<Pubblicazione>-\<Sottoscrittore>-\<intero>**|  
|Agente di distribuzione per le sottoscrizioni push|**\<ServerPubblicazione>-\<DatabasePubblicazione>-\<Pubblicazione>-\<Sottoscrittore>-\<intero>** <sup>1</sup>|  
|Agente di distribuzione per le sottoscrizioni pull|**\<ServerPubblicazione>-\<DatabasePubblicazione>-\<Pubblicazione>-\<Sottoscrittore>-\<DatabaseSottoscrizione>-\<GUID>** <sup>2</sup>|  
|Agente di distribuzione per le sottoscrizioni push di Sottoscrittori non SQL Server|**\<ServerPubblicazione>-\<DatabasePubblicazione>-\<Pubblicazione>-\<Sottoscrittore>-\<intero>**|  
|Agente di lettura coda|**[\<DatabaseDistribuzione>].\<intero>**|  
  
 <sup>1</sup> per le sottoscrizioni push a pubblicazioni Oracle, è il nome del processo  **\<pubblicazione >-\<server di pubblicazione**> anziché  **\<Publisher >-\< Databasepubblicazione >**.  
  
 <sup>2</sup> per le sottoscrizioni pull a pubblicazioni Oracle, è il nome del processo  **\<pubblicazione >-\<DistributionDatabase**> anziché  **\<Publisher >-\< Databasepubblicazione >**.  
  
 Durante la configurazione della replica si specificano gli account utilizzati per l'esecuzione degli agenti. Tutti i passaggi del processo, tuttavia, vengono eseguiti nel contesto di sicurezza di un *proxy*e pertanto la replica esegue internamente i mapping seguenti per gli account dell'agente specificati:  
  
-   Viene innanzitutto eseguito il mapping tra l'account e una credenziale utilizzando l'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] [CREATE CREDENTIAL](/sql/t-sql/statements/create-credential-transact-sql) statement. I proxy di[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent utilizzano le credenziali per archiviare le informazioni sugli account utente di Windows.  
  
-   Viene chiamata la stored procedure [sp_add_proxy](/sql/relational-databases/system-stored-procedures/sp-add-proxy-transact-sql) e le credenziali vengono utilizzate per creare un proxy.  
  
> [!NOTE]  
>  Queste informazioni vengono fornite allo scopo di illustrare i processi richiesti per l'esecuzione degli agenti nel contesto di sicurezza appropriato. Non è in genere necessario interagire direttamente con le credenziali o i proxy creati.  
  
## <a name="see-also"></a>Vedere anche  
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [Sicurezza della replica di SQL Server](view-and-modify-replication-security-settings.md)   
 [Proteggere la cartella snapshot](secure-the-snapshot-folder.md)  
  
  
