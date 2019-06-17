---
title: Configurare gli account del servizio (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services], logon accounts
- logon accounts [Analysis Services]
- accounts [Analysis Services]
- logon accounts [Analysis Services], about logon accounts
ms.assetid: b481bd51-e077-42f6-8598-ce08c1a38716
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8dfde906f7cadc01b9c7a4abbe32be1bd0408986
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080193"
---
# <a name="configure-service-accounts-analysis-services"></a>Configurare gli account del servizio (Analysis Services)
  Il provisioning dell'account a livello di prodotto è documentato in [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md), un argomento che fornisce informazioni complete sull'account del servizio per tutti i servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tra cui [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Fare riferimento a questo argomento per ottenere informazioni sui tipi di account validi, sui privilegi di Windows assegnati dal programma di installazione, sulle autorizzazioni per il file system e il Registro di sistema e altro ancora.  
  
 Questo argomento fornisce informazioni aggiuntive per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], tra cui le autorizzazioni aggiuntive necessarie per le installazioni tabulari e cluster. Descrive inoltre le autorizzazioni necessarie per supportare le operazioni del server. Ad esempio, è possibile configurare operazioni di elaborazione e query da eseguire con l'account del servizio, nel qual caso però sarà necessario concedere alcune autorizzazioni aggiuntive.  
  
-   [Privilegi di Windows assegnati ad Analysis Services](#bkmk_winpriv)  
  
-   [Autorizzazioni per il file system assegnate ad Analysis Services](#bkmk_FilePermissions)  
  
-   [Concessione di ulteriori autorizzazioni per operazioni del server specifiche](#bkmk_tasks)  
  
 Un altro passaggio di configurazione, non descritto in questo articolo, consiste nel registrare un nome dell'entità servizio (SPN) per l'account del servizio e l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Questo passaggio abilita l'autenticazione pass-through dalle applicazioni client alle origini dati di backend in scenari con doppio hop. Questo passaggio è valido solo per i servizi configurati per la delega vincolata Kerberos. Per altre istruzioni, vedere [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md) .  
  
## <a name="logon-account-recommendations"></a>Indicazioni sull'account di accesso  
 In un cluster di failover, tutte le istanze di Analysis Services devono essere configurate per usare un account utente di dominio Windows. Assegnare lo stesso account a tutte le istanze. Per altre informazioni, vedere [Come eseguire il clustering di Analysis Services](https://msdn.microsoft.com/library/dn736073.aspx) .  
  
 Le istanze autonome devono usare l'account virtuale predefinito **NT Service\MSSQLServerOLAPService** per l'istanza predefinita o **NT Service\MSOLAP$** _nome-istanza_ per un'istanza denominata. Questa indicazione si applica alle istanze di Analysis Services in tutte le modalità del server, presupponendo che venga usato Windows Server 2008 R2 e versioni successive per il sistema operativo e SQL Server 2012 e versioni successive per Analysis Services.  
  
## <a name="granting-permissions-to-analysis-services"></a>Concessione di autorizzazioni ad Analysis Services  
 Questa sezione illustra le autorizzazioni richieste da Analysis Services per le operazioni interne locali come, ad esempio, avviare l'eseguibile, leggere il file di configurazione e caricare i database dalla directory dati. Per le indicazioni sull'impostazione delle autorizzazioni per l'accesso ai dati esterni e l'interoperabilità con altri servizi e applicazioni, vedere invece [Concessione di ulteriori autorizzazioni per operazioni del server specifiche](#bkmk_tasks) più avanti in questo argomento.  
  
 Per le operazioni interne, il proprietario delle autorizzazioni in Analysis Services non è l'account di accesso, ma un gruppo di sicurezza di Windows locale creato dal programma di installazione che contiene il SID per servizio. L'assegnazione delle autorizzazioni al gruppo di sicurezza è coerente con le versioni precedenti di Analysis Services. Inoltre, gli account di accesso possono cambiare nel tempo, mentre il SID per servizio e il gruppo di sicurezza locale sono costanti per la durata dell'installazione del server. In Analysis Services è quindi preferibile usare il gruppo di sicurezza anziché l'account di accesso per la gestione delle autorizzazioni. Ogni volta che si concedono manualmente i diritti all'istanza del servizio, indipendentemente dal fatto che si tratti di autorizzazioni del file system o di privilegi di Windows, assicurarsi di concedere le autorizzazioni al gruppo di sicurezza locale creato per l'istanza del server.  
  
 Il nome del gruppo di sicurezza segue uno schema specifico. Il prefisso è sempre `SQLServerMSASUser$`, seguito dal nome del computer, terminando con il nome dell'istanza. L'istanza predefinita è `MSSQLSERVER`. Un'istanza denominata è il nome assegnato durante la configurazione.  
  
 È possibile visualizzare questo gruppo di sicurezza nelle impostazioni di sicurezza locali:  
  
-   Eseguire compmgmt. msc | **Utenti e gruppi locali** | **gruppi** | `SQLServerMSASUser$`\<server-name >`$MSSQLSERVER` (per un'istanza predefinita).  
  
-   Fare doppio clic sul gruppo di sicurezza per visualizzarne i membri.  
  
 L'unico membro del gruppo è il SID per servizio. Subito dopo c'è l'account di accesso. Il nome dell'account di accesso è generico; serve per fornire il contesto al SID per servizio. Se successivamente si modifica l'account di accesso e quindi si torna a questa pagina, si noterà che il gruppo di sicurezza e il SID per servizio non cambiano, ma l'etichetta dell'account di accesso è diversa.  
  
##  <a name="bkmk_winpriv"></a> Privilegi di Windows assegnati all'account del servizio Analysis Services  
 Analysis Services deve ottenere le autorizzazioni dal sistema operativo per l'avvio del servizio e per richiedere le risorse di sistema. I requisiti variano in base alla modalità del server e a seconda se l'istanza è di tipo cluster. Se non si ha familiarità con i privilegi di Windows, vedere le pagine [Privileges](https://msdn.microsoft.com/library/windows/desktop/aa379306\(v=vs.85\).aspx) (Privilegi) e [Privilege Constants (Windows)](/windows/desktop/SecAuthZ/privilege-constants) (Costanti relative ai privilegi (Windows)) per informazioni dettagliate.  
  
 Tutte le istanze di Analysis Services richiedono il privilegio **Accesso come servizio** (SeServiceLogonRight). Il programma di installazione di SQL Server assegna il privilegio per l'account del servizio specificato durante l'installazione. Per i server in esecuzione in modalità multidimensionale e di data mining, questo è l'unico privilegio di Windows richiesto dall'account del servizio di Analysis Services per le installazioni di server autonomi ed è l'unico privilegio configurato dal programma di installazione per Analysis Services. Per le istanze cluster e tabulari è necessario aggiungere manualmente ulteriori privilegi di Windows.  
  
 Le istanze del cluster di failover, in modalità tabulare o multidimensionale, devono disporre del privilegio **Aumento della priorità di pianificazione** (SeIncreaseBasePriorityPrivilege).  
  
 Le istanze tabulari usano i seguenti tre privilegi aggiuntivi, che devono essere concessi manualmente dopo l'installazione dell'istanza.  
  
|||  
|-|-|  
|**Aumento di un working set di processo** (SeIncreaseWorkingSetPrivilege)|Questo privilegio è disponibile per tutti gli utenti per impostazione predefinita tramite il gruppo di sicurezza **Utenti** . Se Blocca un server rimuovendo i privilegi per questo gruppo, Analysis Services non venga avviato, registrando l'errore: "Un privilegio richiesto non è disponibile dal client." Quando si verifica questo errore, ripristinare il privilegio in Analysis Services concedendo tale privilegio al gruppo di sicurezza di Analysis Services appropriato.|  
|**Regolazione limite risorse memoria per un processo** (SeIncreaseQuotaSizePrivilege)|Questo privilegio viene usato per richiedere una quantità maggiore di memoria se un processo non dispone di risorse sufficienti per completare l'esecuzione, in base alle soglie di memoria stabilite per l'istanza.|  
|**Blocco di pagine in memoria** (SeLockMemoryPrivilege)|Questo privilegio è necessario solo se il paging è completamente disattivato. Per impostazione predefinita, un'istanza del server tabulare usa il file di paging di Windows, ma è possibile impedirne l'uso impostando `VertiPaqPagingPolicy` su 0.<br /><br /> `VertiPaqPagingPolicy` impostato su 1 (impostazione predefinita) indica all'istanza del server tabulare di usare il file di paging di Windows. Le allocazioni non vengono bloccate consentendo a Windows di eliminare tramite paging le allocazioni in base alle esigenze. Poiché viene usato il paging, non è necessario bloccare le pagine in memoria. Pertanto, per la configurazione predefinita (dove `VertiPaqPagingPolicy` = 1), non è necessario concedere il **blocco di pagine in memoria** privilegio a un'istanza tabulare.<br /><br /> `VertiPaqPagingPolicy` impostato su 0. Se si disattiva il paging per Analysis Services, le allocazioni vengono bloccate, supponendo che all'istanza tabulare venga concesso il privilegio **Blocco di pagine in memoria** . Con questa impostazione e il privilegio **Blocco di pagine in memoria** , Windows non può eliminare tramite paging le allocazioni di memoria effettuate per Analysis Services quando la quantità di memoria disponibile nel sistema è insufficiente. Analysis Services si basa sul **blocco di pagine in memoria** autorizzazione come privilegio `VertiPaqPagingPolicy` = 0. Si noti che non è consigliabile disattivare il paging di Windows. Si aumenta la frequenza di errori di memoria insufficiente per le operazioni che altrimenti potrebbero riuscire se il paging fosse consentito. Visualizzare [Memory Properties](../server-properties/memory-properties.md) per altre informazioni sulle `VertiPaqPagingPolicy`.|  
  
#### <a name="to-view-or-add-windows-privileges-on-the-service-account"></a>Per visualizzare o aggiungere privilegi di Windows per l'account del servizio  
  
1.  Eseguire GPEDIT.msc | Criteri del computer locale | Configurazione computer | Impostazioni di Windows | Impostazioni di sicurezza | Criteri locali | Assegnazione diritti utente.  
  
2.  Verificare i criteri esistenti che includono `SQLServerMSASUser$`. Si tratta di un gruppo di sicurezza locale presente nei computer in cui è installato Analysis Services. A questo gruppo di sicurezza vengono concessi sia i privilegi di Windows che le autorizzazioni alle cartelle di file. Fare doppio clic sul privilegio **Accesso come servizio** per vedere come il gruppo di sicurezza viene specificato nel sistema. Il nome completo del gruppo di sicurezza varia a seconda che Analysis Services sia stato installato come istanza denominata. Quando si aggiungono i privilegi dell'account, usare questo gruppo di sicurezza anziché l'account del servizio effettivo.  
  
3.  Per aggiungere i privilegi dell'account in GPEDIT, fare clic con il pulsante destro del mouse su **Aumento di un working set di processo** e scegliere **Proprietà**.  
  
4.  Fare clic su **Aggiungi utente o gruppo**.  
  
5.  Immettere il gruppo di utenti per l'istanza di Analysis Services. Tenere presente che l'account del servizio è membro di un gruppo di sicurezza locale, per cui è necessario anteporre il nome del computer locale come dominio dell'account.  
  
     Nell'elenco seguente sono riportati due esempi per un'istanza predefinita e un'istanza denominata con nome "Tabular" in un computer con nome "SQL01-WIN12", in cui il nome del computer corrisponde al dominio locale.  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$MSSQLSERVER  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$TABULAR  
  
6.  Ripetere per **Regolazione limite risorse memoria per un processo**e, facoltativamente, per **Blocco di pagine in memoria** o **Aumento della priorità di pianificazione**.  
  
> [!NOTE]  
>  Nelle versioni precedenti del programma di installazione l'account del servizio Analysis Services è stato aggiunto inavvertitamente al gruppo **Performance Log Users** . Anche se questo problema è stato risolto, le installazioni esistenti potrebbero disporre dell'appartenenza a questo gruppo non necessaria. Dal momento che l'account del servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non necessita dell'appartenenza al gruppo **Performance Log Users** , può essere rimosso dal gruppo in questione.  
  
##  <a name="bkmk_FilePermissions"></a> Autorizzazioni per il file system assegnate all'account del servizio Analysis Services  
  
> [!NOTE]  
>  Vedere [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) per un elenco di autorizzazioni associate a ogni cartella di programma.  
>   
>  Vedere [Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md) per informazioni sulle autorizzazioni di file correlati alla configurazione di IIS e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Tutte le autorizzazioni di file system richieste per le operazioni del server, incluse le autorizzazioni necessarie per caricare e scaricare i database da una cartella di dati designata, vengono assegnate dal programma di installazione di SQL Server durante l'installazione.  
  
 Il proprietario delle autorizzazioni per i file di dati, gli eseguibili dei file di programma, i file di configurazioni, i file di log e i file temporanei è un gruppo di sicurezza locale creato dal programma di installazione di SQL Server.  
  
 Per ogni istanza installata viene creato un solo gruppo di sicurezza. Il gruppo di sicurezza è denominato in base all'istanza **SQLServerMSASUser$ MSSQLSERVER** per l'istanza predefinita, o `SQLServerMSASUser$` \<nomeserver >$\<NomeIstanza > per un'istanza denominata. Questo gruppo di sicurezza viene fornito dal programma di installazione con le autorizzazioni per i file necessarie per eseguire le operazioni del server. Se si controllano le autorizzazioni di sicurezza per la directory \MSAS12.MSSQLSERVER\OLAP\BIN, si noterà che il proprietario dell'autorizzazione per la directory in questione è il gruppo di sicurezza, non l'account del servizio né il relativo SID per servizio.  
  
 Nel gruppo di sicurezza è incluso solo un membro, vale a dire il SID per servizio dell'account di avvio dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Il programma di installazione aggiunge il SID per servizio al gruppo di sicurezza locale. L'uso di un gruppo di sicurezza locale con l'appartenenza al SID rappresenta una lieve ma percettibile differenza nel modo in cui il programma di installazione di SQL Server esegue il provisioning di Analysis Services rispetto al Motore di database.  
  
 Se si ritiene che le autorizzazioni per i file siano danneggiate, seguire questi passaggi per verificare la corretta esecuzione del provisioning del servizio:  
  
1.  Usare lo strumento da riga di comando per il controllo del servizio (sc.exe) per ottenere il SID di un'istanza del servizio predefinita.  
  
     `SC showsid MSSqlServerOlapService`  
  
     Per un'istanza denominata, dove il nome dell'istanza è "Tabular", usare questa sintassi:  
  
     `SC showsid MSOlap$Tabular`  
  
2.  Uso **Gestione Computer** | **utenti e gruppi locali** | **gruppi** per controllare l'appartenenza di SQLServerMSASUser$\<nomeserver >$\<NomeIstanza > gruppo di sicurezza.  
  
     Il SID del membro deve corrispondere al SID per servizio del passaggio 1.  
  
3.  Usare **Esplora risorse** | **Programmi** | **Microsoft SQL Server** | MSASxx.MSSQLServer | **OLAP** | **bin** per verificare che al gruppo di sicurezza del passaggio 2 vengano concesse le proprietà di sicurezza della cartella.  
  
> [!NOTE]  
>  Non rimuovere né modificare mai un SID. Per ripristinare un SID per servizio eliminato inavvertitamente, vedere [ https://support.microsoft.com/kb/2620201 ](https://support.microsoft.com/kb/2620201).  
  
 **Altre informazioni sui SID per servizio**  
  
 A ogni account di Windows è associato un [SID](http://en.wikipedia.org/wiki/Security_Identifier), ma anche ai servizi possono essere associati dei SID, definiti pertanto SID per servizio. Un SID per servizio viene creato all'installazione dell'istanza del servizio come elemento univoco, permanente del servizio. Il SID per servizio locale è un SID locale a livello di computer generato dal nome del servizio. In un'istanza predefinita, il relativo nome descrittivo è NT SERVICE\MSSQLServerOLAPService.  
  
 Il vantaggio di un SID per servizio consiste nella possibilità di modificare in modo arbitrario un account di accesso molto ben visibile senza influire sulle autorizzazioni per i file. Si supponga, ad esempio, che siano installate due istanze di Analysis Services, una predefinita e una denominata, entrambe in esecuzione con lo stesso account utente di Windows. Quando l'account di accesso è condiviso, ogni istanza del servizio avrà un SID per servizio univoco. Questo SID è diverso dal SID dell'account di accesso. Il SID per servizio viene usato per le autorizzazioni per i file e i privilegi di Windows. Al contrario, il SID dell'account di accesso viene usato per gli scenari di autenticazione e autorizzazione. Sono quindi SID diversi usati per scopi diversi.  
  
 Poiché il SID non è modificabile, gli ACL del file system creati durante l'installazione del servizio possono essere usati all'infinito, indipendentemente dalla frequenza con cui si modifica l'account del servizio. Come misura di sicurezza aggiuntiva, gli ACL mediante i quali vengono specificate le autorizzazioni tramite un SID garantiscono l'accesso ai file eseguibili del programma e alle cartelle di dati solo da una singola istanza di un servizio, anche se ne vengono eseguiti altri con lo stesso account.  
  
##  <a name="bkmk_tasks"></a> Concessione di ulteriori autorizzazioni di Analysis Services per operazioni del server specifiche  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esegue alcune attività nel contesto di sicurezza dell'account del servizio (o account di accesso) usato per avviare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], mentre esegue altre attività nel contesto di sicurezza dell'utente che richiede l'attività.  
  
 Nella tabella seguente sono descritte le autorizzazioni aggiuntive necessarie per supportare le attività eseguite come account del servizio.  
  
|Operazione del server|Elemento di lavoro|Giustificazione|  
|----------------------|---------------|-------------------|  
|Accesso remoto a origini dati relazionali esterne|Creare un accesso al database per l'account del servizio|L'elaborazione fa riferimento al recupero di dati da un'origine dati esterna, di solito un database relazionale, che viene successivamente caricata in un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Una delle opzioni di credenziali per il recupero di dati esterni consiste nell'utilizzare l'account del servizio. Questa opzione di credenziali funziona solo se si crea un accesso al database per l'account del servizio e si concedono le autorizzazioni di lettura sul database di origine. Vedere [Impostare opzioni di rappresentazione &#40;SSAS - multidimensionale&#41;](../multidimensional-models/set-impersonation-options-ssas-multidimensional.md) per altre informazioni sulla modalità con cui l'opzione account del servizio viene usata per questa attività. Analogamente, se ROLAP viene utilizzato come modalità di archiviazione, sono disponibili le stesse opzioni di rappresentazione. In questo caso, all'account deve inoltre essere associato l'accesso in scrittura ai dati di origine per elaborare le partizioni ROLAP, in altre parole per archiviare le aggregazioni.|  
|DirectQuery|Creare un accesso al database per l'account del servizio|DirectQuery è una funzionalità tabulare utilizzata per eseguire una query sui set di dati esterni che sono troppo grandi per adattarsi al modello tabulare o che presentano altre caratteristiche che rendono DirectQuery una soluzione migliore rispetto all'opzione di archiviazione in memoria predefinita. Una delle opzioni di connessione disponibili nella modalità DirectQuery consiste nell'utilizzo dell'account del servizio. Ancora una volta, questa opzione funziona solo quando l'account del servizio dispone di un accesso al database e delle autorizzazioni di lettura sull'origine dati di destinazione. Vedere [Impostare opzioni di rappresentazione &#40;SSAS - multidimensionale&#41;](../multidimensional-models/set-impersonation-options-ssas-multidimensional.md) per altre informazioni sulla modalità con cui l'opzione account del servizio viene usata per questa attività. In alternativa, è possibile utilizzare le credenziali dell'utente corrente per il recupero dei dati. Nella maggior parte dei casi, per questa opzione è richiesta una connessione a doppio hop, pertanto assicurarsi di configurare l'account del servizio per la delega vincolata Kerberos, affinché sia in grado di delegare identità a un server a valle. Per altre informazioni, vedere [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md).|  
|Accesso remoto ad altre istanze di SSAS|Aggiungere l'account del servizio ai ruoli del database di Analysis Services definiti nel server remoto|Le partizioni remote e gli oggetti collegati di riferimento in altre istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] remote sono entrambi funzionalità del sistema per cui sono richieste autorizzazioni per un dispositivo o computer remoto. Se un utente crea e popola le partizioni remote oppure configura un oggetto collegato, questa operazione viene eseguita nel contesto di sicurezza dell'utente corrente. Se successivamente queste operazioni vengono automatizzate, tramite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] si accederà alle istanze remote nel contesto di sicurezza del relativo account del servizio. Per accedere a oggetti collegati in un'istanza remota di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], è necessario che l'account di accesso disponga dell'autorizzazione per la lettura degli oggetti appropriati nell'istanza remota, ad esempio l'accesso in lettura a dimensioni specifiche. Analogamente, per utilizzare le partizioni remote è necessario che l'account del servizio disponga dei diritti amministrativi per l'istanza remota. Queste autorizzazioni vengono concesse per l'istanza di Analysis Services remota, utilizzando ruoli mediante i quali vengono associate operazioni consentite a un oggetto specifico. Per le istruzioni su come concedere le autorizzazioni di Controllo completo che consentono le operazioni di elaborazione e query, vedere [Concedere le autorizzazioni per il database &#40;Analysis Services&#41;](../multidimensional-models/grant-database-permissions-analysis-services.md). Vedere [Creare e gestire una partizione remota &#40;Analysis Services&#41;](../multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md) per altre informazioni sulle partizioni remote.|  
|Writeback|Aggiungere l'account del servizio ai ruoli del database di Analysis Services definiti nel server remoto|Se abilitato in applicazioni client, il writeback è una funzionalità dei modelli multidimensionali che consente la creazione di nuovi valori dei dati durante la relativa analisi. Se il writeback è abilitato in una dimensione o in un cubo, l'account del servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve disporre di autorizzazioni di scrittura per la tabella writeback nel database relazionale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di origine. Se questa tabella non è già presente e deve essere creata, è necessario che l'account del servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] disponga inoltre di autorizzazioni per la creazione della tabella all'interno del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] designato.|  
|Scrittura di una tabella del log di query in un database relazionale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Creare un accesso al database per l'account del servizio e assegnare le autorizzazioni di scrittura sulla tabella del log di query|È possibile abilitare la registrazione delle query per raccogliere i dati di utilizzo in una tabella di database per una successiva analisi. L'account del servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve disporre di autorizzazioni di scrittura per la tabella del log di query nel database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] designato. Se tale tabella non è già presente e deve essere creata, è necessario che l'account di accesso di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] disponga inoltre di autorizzazioni per la creazione della tabella all'interno del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] designato. Per altre informazioni, vedere i post dei blog [Improve SQL Server Analysis Services Performance with the Usage Based Optimization Wizard (Blog)](http://www.mssqltips.com/sqlservertip/2876/improve-sql-server-analysis-services-performance-with-the-usage-based-optimization-wizard/) (Miglioramento delle prestazioni di SQL Server Analysis Services con l'Ottimizzazione guidata basata sulle statistiche di utilizzo) e [Query Logging in Analysis Services (Blog)](http://weblogs.asp.net/miked/archive/2013/07/31/query-logging-in-analysis-services.aspx)(Registrazione delle query in Analysis Services).|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Account del servizio SQL Server e SID per servizio (blog)](http://www.travisgan.com/2013/06/sql-server-service-account-and-per.html)   
 [SQL Server utilizza un SID di servizio per fornire l'isolamento dei servizi (articolo KB)](https://support.microsoft.com/kb/2620201)   
 [Token di accesso (MSDN)](/windows/desktop/SecAuthZ/access-tokens)   
 [ID di sicurezza (MSDN)](/windows/desktop/SecAuthZ/security-identifiers)   
 [Token di accesso (Wikipedia)](http://en.wikipedia.org/wiki/Access_token)   
 [Elenchi di controllo di accesso (Wikipedia)](http://en.wikipedia.org/wiki/Access_control_list)  
  
  
