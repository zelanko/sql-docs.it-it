---
title: Registrare un'istanza di SQL Server (Utilità SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.SWB.makemanaged.agentaccount.F1
- sql13.SWB.makemanaged.welcome.F1
- sql13.SWB.makemanaged.enrolling.F1
- sql13.SWB.makemanaged.instancename.F1
- sql13.SWB.makemanaged.Summary.F1
- sql13.SWB.makemanaged.progress.F1
- sql13.SWB.makemanaged.validation.F1
helpviewer_keywords:
- Enroll instance
ms.assetid: a801c619-611b-4e82-a8d8-d1e01691b7a1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: dda51dd5449719aedd7697310c1f7befe3ee1390
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68115423"
---
# <a name="enroll-an-instance-of-sql-server-sql-server-utility"></a>Registrare un'istanza di SQL Server (Utilità SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile registrare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un'utilità esistente di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per monitorarne le prestazioni e la configurazione come istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il punto di controllo dell'utilità raccoglie informazioni sulla configurazione e sulle prestazioni delle istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ogni 15 minuti. Queste informazioni vengono archiviate nel data warehouse di gestione dell'utilità (UMDW) nel punto di controllo dell'utilità; il nome del file UMDW è sysutility_mdw. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono confrontati con i criteri per consentire l'identificazione di colli di bottiglia nell'utilizzo delle risorse e le possibilità di consolidamento.  
  
 In questa versione il punto di controllo dell'utilità e tutte le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono soddisfare i requisiti seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere la versione 10.50 o successiva.  
  
-   L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere di tipo [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve funzionare all'interno di un solo dominio Windows o in domini con relazioni di trust bidirezionali.  
  
-   Gli account del servizio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il punto di controllo dell'utilità e per tutte le istanze gestite di SQL Server devono disporre dell'autorizzazione di lettura impostata per gli utenti in Active Directory.  
  
-   L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da registrare non può essere SQL Azure.  
  
 In questa versione il punto di controllo dell'utilità deve soddisfare i requisiti seguenti:  
  
-   L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere un'edizione supportata. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
-   È consigliabile collocare il punto di controllo dell'utilità in un'istanza di SQL Server che applica la distinzione tra maiuscole e minuscole.  
  
-   Per la pianificazione della capacità del computer del punto di controllo dell'utilità, tenere presenti i seguenti consigli:  
  
    -   In uno scenario tipico lo spazio su disco utilizzato dal database UMDW (sysutility_mdw) nel punto di controllo dell'utilità è di circa 2 GB per istanza gestita di SQL Server per anno. Questa stima può variare a seconda del numero di oggetti di database e di sistema raccolti dall'istanza gestita. Lo spazio occupato su disco da UMDW (sysutility_mdw) aumenta più rapidamente durante i primi due giorni.  
  
    -   In uno scenario tipico lo spazio su disco utilizzato dal database msdb nel punto di controllo dell'utilità è di circa 20 MB per istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si tenga presente che questa stima può variare a seconda dei criteri di utilizzo delle risorse e del numero di oggetti di database e di sistema raccolti dall'istanza gestita. In generale, l'utilizzo dello spazio su disco aumenta con l'aumentare del numero di violazioni dei criteri e della durata dell'intervallo di tempo per le risorse volatili.  
  
    -   Si noti che la rimozione di un'istanza gestita dal punto di controllo dell'utilità non riduce lo spazio su disco utilizzato dai database del punto di controllo dell'utilità fino allo scadere dei periodi di memorizzazione dei dati per l'istanza gestita.  
  
 In questa versione tutte le istanze gestite di SQL Server devono soddisfare i requisiti seguenti:  
  
-   Se il punto di controllo dell'utilità è ospitato in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]che non applica la distinzione tra maiuscole e minuscole, è consigliabile che anche le istanze gestite di SQL Server non applichino la distinzione tra maiuscole e minuscole.  
  
-   I dati FILESTREAM non sono supportati per il monitoraggio di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per altre informazioni, vedere [Specifiche di capacità massima per SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md) e [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Per altre informazioni sui concetti di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
> [!IMPORTANT]  
>  L'esecuzione side-by-side del set di raccolta di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dei set di raccolta non appartenenti a Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è supportata. Ciò significa che un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere monitorata da altri set di raccolta anche se l'istanza è membro di un'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si noti tuttavia che tutti i set di raccolta sull'istanza gestita caricheranno i propri dati nel data warehouse di gestione dell'utilità. Per altre informazioni, vedere [Considerazioni per l'esecuzione di set di raccolta dell'utilità e non appartenenti all'utilità nella stessa istanza di SQL Server](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md) e [Configure Your Utility Control Point Data Warehouse &#40;SQL Server Utility&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md) (Configurare il data warehouse del punto di controllo dell'utilità -Utilità SQL Server).  
  
## <a name="wizard-steps"></a>Passaggi della procedura guidata  
 Nelle sezioni seguenti sono fornite informazioni dettagliate su ogni pagina del flusso di lavoro della procedura guidata. Fare clic su un collegamento nell'elenco riportato di seguito per passare ai dettagli per una pagina della procedura guidata: Per altre informazioni su uno script di PowerShell per questa operazione, vedere l' [esempio](#PowerShell_enroll)relativo a PowerShell.  
  
-   [Introduzione alla procedura guidata Registra istanza](#Welcome)  
  
-   [Specificare l'istanza di SQL Server](#Instance_name)  
  
-   [Finestra di dialogo della connessione](#Connection_dialog)  
  
-   [Account set di raccolta utilità](#Proxy_configuration)  
  
-   [Convalida istanza di SQL Server](#Validation_rules)  
  
-   [Riepilogo della registrazione dell'istanza](#Summary)  
  
-   [Registrazione dell'istanza di SQL Server](#Enrolling)  
  
##  <a name="introduction-to-enroll-instance-wizard"></a><a name="Welcome"></a> Introduzione alla procedura guidata Registra istanza  
 Per avviare la procedura guidata, espandere l'albero in Esplora utilità fino a visualizzare un punto di controllo dell'utilità, fare clic con il pulsante destro del mouse su **Istanze gestite** e scegliere **Aggiungi istanza gestita**.  
  
 Scegliere **Avanti**per continuare.  
  
##  <a name="specify-the-instance-of-sql-server"></a><a name="Instance_name"></a> Specificare l'istanza di SQL Server  
 Per selezionare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dalla finestra di dialogo della connessione, fare clic su **Connetti**. Specificare il nome del computer e il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel formato NomeComputer\NomeIstanza. Per altre informazioni, vedere [Connetti al server &#40;Motore di database&#41;](https://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41).  
  
 Scegliere **Avanti**per continuare.  
  
##  <a name="connection-dialog"></a><a name="Connection_dialog"></a> Finestra di dialogo di connessione  
 Nella finestra di dialogo Connetti al server, verificare il tipo di server, il nome del computer e il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Connetti al server &#40;Motore di database&#41;](https://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41).  
  
> [!NOTE]  
>  Se la connessione è crittografata, verrà utilizzata tale connessione. Se la connessione non è crittografata, Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si riconnetterà utilizzando una connessione crittografata.  
  
 Per continuare, fare clic su **Connetti**.  
  
##  <a name="utility-collection-set-account"></a><a name="Proxy_configuration"></a> Account set di raccolta utilità  
 Specificare un account di dominio di Windows per eseguire il set di raccolta di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questo account viene utilizzato come account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per il set di raccolta di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In alternativa, è possibile utilizzare l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esistente. Per soddisfare i requisiti della convalida, utilizzare le linee guida seguenti per specificare l'account.  
  
 Se si specifica l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent:  
  
-   L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere un account di dominio di Windows che non è un account incorporato come LocalSystem, NetworkService o LocalService.  
  
 Scegliere **Avanti**per continuare.  
  
##  <a name="sql-server-instance-validation"></a><a name="Validation_rules"></a> Convalida istanza di SQL Server  
 In questa versione le condizioni seguenti devono essere vere affinché l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] venga registrata in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Condizione|Azione correttiva|  
|---------------|-----------------------|  
|È necessario avere i privilegi di amministratore per l'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il punto di controllo dell'utilità.|Accedere con un account con privilegi di amministratore per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificata e per il punto di controllo dell'utilità.|  
|L'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve supportare la registrazione dell'istanza.|Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|TCP/IP deve essere abilitato nel punto di controllo dell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Abilitare TCP/IP nel punto di controllo dell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può essere già registrata con nessun altro punto di controllo dell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificata è già gestita come parte di un'istanza di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esistente, non è possibile registrarla con un altro punto di controllo dell'utilità.|  
|L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può essere già un punto di controllo dell'utilità.|Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificata è già un punto di controllo dell'utilità diverso dal punto di controllo dell'utilità al quale si è connessi, non è possibile registrarla in questo punto di controllo dell'utilità.|  
|L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve avere set di raccolta di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installati.|Ripetere l'installazione dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|È necessario arrestare i set di raccolta nell'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Arrestare i set di raccolta preesistenti nell'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se l'agente di raccolta dati è disabilitato, abilitarlo, arrestare qualsiasi set di raccolta dati eseguito, quindi eseguire nuovamente le regole di convalida per l'operazione di creazione del punto di controllo dell'utilità.<br /><br /> Per abilitare l'agente di raccolta dati:<br /><br /> In Esplora oggetti espandere il nodo **Gestione** .<br /><br /> Fare clic con il pulsante destro del mouse su **Raccolta dati**, quindi scegliere **Abilita raccolta dati**.<br /><br /> Per arrestare un set di raccolta:<br /><br /> In Esplora oggetti espandere il nodo Gestione, espandere **Raccolta dati**, quindi **Set di raccolta dati di sistema**.<br /><br /> Fare clic con il pulsante destro del mouse sul set di raccolta che si vuole arrestare e quindi scegliere **Arresta set di raccolta dati**.<br /><br /> In una finestra di messaggio verrà visualizzato il risultato di questa azione, mentre un cerchio rosso sull'icona del set di raccolta indicherà che il set di raccolta è stato arrestato.|  
|È necessario avviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nell'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Avviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sull'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se l'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , configurare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in modo che venga avviato manualmente. In caso contrario, configurare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in modo che venga avviato automaticamente.|  
|È necessario che il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nel punto di controllo dell'utilità sia avviato.|Avviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nel punto di controllo dell'utilità. Se il punto di controllo dell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , configurare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in modo che venga avviato manualmente. In caso contrario, configurare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in modo che venga avviato automaticamente.|  
|È necessario configurare correttamente WMI.|Per risolvere i problemi di configurazione WMI, vedere [Attività e funzionalità di Utilità SQL Server](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453).|  
|L'account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere un account di dominio di Windows valido nel punto di controllo dell'utilità.|Specificare un account di dominio di Windows valido. Per verificare che l'account sia valido, accedere al punto di controllo dell'utilità utilizzando l'account di dominio di Windows.|  
|Se si seleziona l'opzione relativa all'account proxy, l'account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere un account di dominio di Windows valido nell'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Specificare un account di dominio di Windows valido. Per verificare che l'account sia valido, accedere all'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'account di dominio di Windows.|  
|L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non può essere un account incorporato, come Servizio di rete.|Assegnare nuovamente l'account a un account di dominio di Windows. Per verificare che l'account sia valido, accedere all'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'account di dominio di Windows.|  
|L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere un account di dominio di Windows valido nel punto di controllo dell'utilità.|Specificare un account di dominio di Windows valido. Per verificare che l'account sia valido, accedere al punto di controllo dell'utilità utilizzando l'account di dominio di Windows.|  
|Se si seleziona l'opzione relativa all'account del servizio, l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere un account di dominio di Windows valido nell'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Specificare un account di dominio di Windows valido. Per verificare che l'account sia valido, accedere all'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'account di dominio di Windows.|  
  
 Se alcune condizioni hanno dato risultati negativi nella convalida, correggere i problemi rilevati, quindi fare clic su **Riesegui convalida** per verificare la configurazione del computer.  
  
 Per salvare il report di convalida, fare clic su **Salva report** , quindi specificare un percorso per il file.  
  
 Scegliere **Avanti**per continuare.  
  
##  <a name="summary-of-instance-enrollment"></a><a name="Summary"></a> Riepilogo della registrazione dell'istanza  
 Nella pagina di riepilogo sono elencate informazioni sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da aggiungere a Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Impostazioni istanza gestita  
  
-   Nome istanza di SQL Server: NomeComputer\NomeIstanza  
  
-   Account set di raccolta utilità: NomeDominio\NomeUtente  
  
 Scegliere **Avanti**per continuare.  
  
##  <a name="enrolling-the-instance-of-sql-server"></a><a name="Enrolling"></a> Registrazione dell'istanza di SQL Server  
 Nella pagina di registrazione viene indicato lo stato dell'operazione:  
  
-   Preparazione dell'istanza per la registrazione.  
  
-   Creazione della directory cache per i dati raccolti.  
  
-   Configurazione del set di raccolta dell'utilità.  
  
 Per salvare un report sull'operazione di registrazione, fare clic su **Salva report** , quindi specificare un percorso per il file.  
  
 Per completare la procedura guidata, fare clic su **Fine**.  
  
> [!NOTE]  
>  Se si utilizza l'Autenticazione di SQL Server per connettersi all'istanza di SQL Server per eseguire la registrazione e si specifica un account proxy che appartiene a un dominio Active Directory diverso dal dominio in cui si trova il punto di controllo dell'utilità, la convalida dell'istanza riesce, ma l'operazione di registrazione non riesce con il messaggio di errore seguente:  
>   
>  Eccezione durante l'esecuzione di un'istruzione o un batch Transact-SQL. (Microsoft.SqlServer.ConnectionInfo)  
>   
>  Ulteriori informazioni:  Impossibile ottenere informazioni relative al gruppo/utente di Windows NT '\<NomeDominio\NomeAccount>', codice di errore 0x5. (Microsoft SQL Server, Errore: 15404)  
>   
>  Per altre informazioni sulla risoluzione di questo errore, vedere [Attività e funzionalità di Utilità SQL Server](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453).  
  
> [!IMPORTANT]  
>  Non modificare le proprietà del set di raccolta "Informazioni utilità" in un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non abilitare/disabilitare manualmente la raccolta dati, in quanto viene controllata da un processo dell'agente Utilità.  
  
 Dopo avere completato la Registrazione guidata istanza, fare clic sul nodo **Istanze gestite** nel riquadro di navigazione di **Esplora utilità** in SSMS. Le istanze registrate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono visualizzate nella visualizzazione elenco nel riquadro **Contenuto Esplora utilità** .  
  
 Il processo di raccolta dati inizia immediatamente, ma possono essere necessari fino a 30 minuti affinché i dati vengano visualizzati nel dashboard e i punti di visualizzazione nel riquadro del contenuto Esplora utilità. La raccolta dati continua una volta ogni 15 minuti. Per aggiornare i dati, fare clic con il pulsante destro del mouse sul nodo **Istanze gestite** nel riquadro di navigazione di **Esplora utilità**, scegliere quindi **Aggiorna[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o fare clic con il pulsante destro del mouse sul nome dell'istanza di** nella visualizzazione elenco, quindi scegliere **Aggiorna**.  
  
 Per rimuovere le istanze gestite da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selezionare **Istanze gestite** nel riquadro di navigazione di **Esplora utilità** per popolare la visualizzazione elenco di istanze gestite, fare clic con il pulsante destro del mouse sul nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella visualizzazione elenco in **Contenuto Esplora utilità** , quindi scegliere **Rendi istanza non gestita**.  
  
##  <a name="enroll-an-instance-of-sql-server-using-powershell"></a><a name="PowerShell_enroll"></a> Registrazione di un'istanza di SQL Server tramite PowerShell  
 Usare l'esempio seguente per registrare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un'istanza di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esistente:  
  
```  
> $UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
> $SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
> $Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($SqlStoreConnection);  
> $Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\ManagedInstanceName";  
> $InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
> $ManagedInstance = $Utility.EnrollInstance($InstanceConnection, "ProxyAccount", "ProxyPassword");  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Monitoraggio di istanze di SQL Server in Utilità SQL Server](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Attività e funzionalità di Utilità SQL Server](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
