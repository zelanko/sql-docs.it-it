---
title: Creare un punto di controllo di Utilità SQL Server (Utilità SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.create.ucp.progress.F1
- SQL12.SWB.create.ucp.welcome.F1
- SQL12.SWB.create.ucp.Summary.F1
- SQL12.SWB.create.ucp.validation.F1
- SQL12.SWB.create.ucp.instancename.F1
- SQL12.SWB.create.ucp.agentconfiguration.F1
helpviewer_keywords:
- Create UCP
- UCP
ms.assetid: d5335124-1625-47ce-b4ac-36078967158c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: db76db817561095b7b09b1a86e7c2ca10ec9174a
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798093"
---
# <a name="create-a-sql-server-utility-control-point-sql-server-utility"></a>Creazione di un punto di controllo dell'utilità di SQL Server (Utilità SQL Server)
  Un'azienda può disporre di più Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ogni Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può gestire molte istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e applicazioni livello dati. Ogni istanza di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone di un solo punto di controllo dell'utilità. È necessario creare un nuovo punto di controllo dell'utilità per Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ogni istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ogni applicazione livello dati è membro di una sola utilità di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed è gestita da un singolo punto di controllo dell'utilità.  
  
 Il punto di controllo dell'utilità raccoglie informazioni sulla configurazione e sulle prestazioni delle istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ogni 15 minuti. Queste informazioni vengono archiviate nel data warehouse di gestione dell'utilità (UMDW) nel punto di controllo dell'utilità; il nome del file UMDW è sysutility_mdw. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono confrontati con i criteri per consentire l'identificazione di colli di bottiglia nell'utilizzo delle risorse e le possibilità di consolidamento.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Prima di creare un punto di controllo dell'utilità, esaminare i requisiti e le indicazioni seguenti.  
  
 In questa versione il punto di controllo dell'utilità e tutte le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono soddisfare i requisiti seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere la versione 10.50 o successiva.  
  
-   L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere di tipo [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve funzionare all'interno di un solo dominio Windows o in domini con relazioni di trust bidirezionali.  
  
-   Gli account del servizio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il punto di controllo dell'utilità e per tutte le istanze gestite di SQL Server devono disporre dell'autorizzazione di lettura impostata per gli utenti in Active Directory.  
  
 In questa versione il punto di controllo dell'utilità deve soddisfare i requisiti seguenti:  
  
-   L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere un'edizione supportata. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   È consigliabile collocare il punto di controllo dell'utilità in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]che applica la distinzione tra maiuscole e minuscole.  
  
 Per la pianificazione della capacità del computer del punto di controllo dell'utilità, tenere presenti i seguenti consigli:  
  
-   In uno scenario tipico lo spazio su disco utilizzato dal database UMDW (sysutility_mdw) nel punto di controllo dell'utilità è di circa 2 GB per istanza gestita di SQL Server per anno. Questa stima può variare a seconda del numero di oggetti di database e di sistema raccolti dall'istanza gestita. Lo spazio occupato su disco da UMDW (sysutility_mdw) aumenta più rapidamente durante i primi due giorni.  
  
-   In uno scenario tipico lo spazio su disco utilizzato dal database msdb nel punto di controllo dell'utilità è di circa 20 MB per istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si tenga presente che questa stima può variare a seconda dei criteri di utilizzo delle risorse e del numero di oggetti di database e di sistema raccolti dall'istanza gestita. In generale, l'utilizzo dello spazio su disco aumenta con l'aumentare del numero di violazioni dei criteri e della durata dell'intervallo di tempo per le risorse volatili.  
  
-   Si noti che la rimozione di un'istanza gestita dal punto di controllo dell'utilità non riduce lo spazio su disco utilizzato dai database del punto di controllo dell'utilità fino allo scadere dei periodi di memorizzazione dei dati per l'istanza gestita.  
  
 In questa versione tutte le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono soddisfare i requisiti seguenti:  
  
-   Se il punto di controllo dell'utilità è ospitato in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]che non applica la distinzione tra maiuscole e minuscole, è consigliabile che anche le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non applichino la distinzione tra maiuscole e minuscole.  
  
-   I dati FILESTREAM non sono supportati per il monitoraggio di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per ulteriori informazioni, vedere la pagina relativa alle [specifiche di capacità massima per SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md) e [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
### <a name="remove-previous-utility-control-points-before-installing-a-new-one"></a>Rimuovere i punti di controllo dell'utilità precedenti prima di installarne uno nuovo  
 Per installare un punto di controllo dell'utilità in un'istanza di SQL Server precedentemente configurata come punto di controllo dell'utilità è necessario innanzitutto rimuovere tutte le istanze gestite di SQL Server e rimuovere il punto di controllo dell'utilità. A questo scopo, eseguire la stored procedure **sp_sysutility_ucp_remove** .  
  
 Prima di eseguire la stored procedure, tenere presente i requisiti seguenti:  
  
-   È necessario eseguire la procedura in un computer configurato come punto di controllo dell'utilità.  
  
-   La procedura deve essere eseguita da un utente che disponga di autorizzazioni sysadmin, le stesse necessarie per la creazione di un punto di controllo dell'utilità.  
  
-   Tutte le istanze gestite di SQL Server devono essere rimosse dal punto di controllo dell'utilità, che rappresenta un'istanza gestita di SQL Server. Per ulteriori informazioni, vedere [Procedura: Rimozione di un'istanza di SQL Server da Utilità SQL Server](https://go.microsoft.com/fwlink/?LinkId=169392).  
  
 Utilizzare questa procedura per rimuovere un punto di controllo dell'utilità di SQL Server da Utilità SQL Server. Al termine dell'operazione sarà nuovamente possibile creare un punto di controllo dell'utilità nell'istanza di SQL Server.  
  
 Utilizzare SQL Server Management Studio per connettersi al punto di controllo dell'utilità, quindi eseguire lo script seguente:  
  
```sql
EXEC msdb.dbo.sp_sysutility_ucp_remove;  
```  
  
> [!NOTE]  
>  Se l'istanza di SQL Server in cui è stato rimosso il punto di controllo dell'utilità dispone di un set di raccolta dati non appartenente all'utilità, il database sysutility_mdw non viene eliminato dalla procedura. In tal caso, è necessario eliminare manualmente il database sysutility_mdw prima di creare nuovamente il punto di controllo dell'utilità.  
  
 Ogni istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ogni applicazione livello dati è membro di una sola utilità di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed è gestita da un singolo punto di controllo dell'utilità. Per altre informazioni sui concetti di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Attività e funzionalità di Utilità SQL Server](sql-server-utility-features-and-tasks.md).  
  
 Un punto di controllo dell'utilità è il punto centrale ragionevole di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Utilizzando il punto di controllo dell'utilità, è possibile visualizzare le informazioni sulla configurazione e sulle prestazioni raccolte dalle istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dalle applicazioni livello dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed eseguire attività generali di pianificazione della capacità. Il punto di controllo dell'utilità è il punto di avvio per la registrazione e la rimozione di istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Dopo aver registrato le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è possibile monitorare l'integrità delle risorse per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le applicazioni del livello dati per identificare le opportunità di consolidamento e isolare i colli di bottiglia delle risorse. Per altre informazioni, vedere [Monitoraggio di istanze di SQL Server in Utilità SQL Server](monitor-instances-of-sql-server-in-the-sql-server-utility.md).  
  
> [!IMPORTANT]  
>  L'esecuzione side-by-side del set di raccolta di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dei set di raccolta non appartenenti a Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è supportata. Ciò significa che un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere monitorata da altri set di raccolta anche se l'istanza è membro di un'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si noti tuttavia che tutti i set di raccolta sull'istanza gestita caricheranno i propri dati nel data warehouse di gestione di Utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Considerazioni per l'esecuzione di set di raccolta dell'utilità e non appartenenti all'utilità nella stessa istanza di SQL Server](run-utility-and-non-utility-collection-sets-on-same-sql-instance.md) e [Configure Your Utility Control Point Data Warehouse &#40;SQL Server Utility&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md) (Configurare il data warehouse del punto di controllo dell'utilità -Utilità SQL Server).  
  
## <a name="wizard-steps"></a>Passaggi della procedura guidata  
 ![](../../database-engine/media/create-ucp.gif "Create_UCP")  
  
 Nelle sezioni seguenti sono fornite le informazioni su ogni pagina del flusso di lavoro della procedura guidata per creare un nuovo punto di controllo dell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per avviare la procedura guidata per creare un nuovo punto di controllo dell'utilità, aprire il riquadro Esplora utilità dal menu Visualizza in SSMS, ![](../../database-engine/media/create-ucp.gif "Create_UCP") quindi fare clic sul pulsante **Crea** punto di controllo dell'utilità nella parte superiore del riquadro Esplora utilità.  
  
 Fare clic su un collegamento nell'elenco riportato di seguito per passare ai dettagli per una pagina della procedura guidata.  
  
 Per ulteriori informazioni su uno script di PowerShell per questa operazione, vedere l' [esempio](#PowerShell_create_UCP).  
  
-   [Introduzione alla procedura guidata Crea punto di controllo dell'utilità](#Welcome)  
  
-   [Specifica istanza](#Instance_name)  
  
-   [Finestra di dialogo della connessione](#Connection_dialog)  
  
-   [Account set di raccolta utilità](#Agent_configuration)  
  
-   [Regole di convalida](#Validation_rules)  
  
-   [Riepilogo](#Summary)  
  
-   [Creazione del punto di controllo dell'utilità](#Creating_UCP)  
  
##  <a name="Welcome"></a> Introduzione alla procedura guidata Crea punto di controllo dell'utilità  
 Se si apre Esplora utilità e non è presente alcun punto di controllo dell'utilità connesso, è necessario connettersi a uno di quelli presenti o crearne uno nuovo.  
  
 **Connettersi a** un punto di controllo dell'utilità esistente: se è già presente un punto di controllo dell'utilità nella distribuzione, è possibile ![ ](../../database-engine/media/connect-to-utility.gif "Connetti a utilità")connettersi a esso facendo clic sul pulsante **Connetti a utilità** nella parte superiore del riquadro Esplora utilità. Per connettersi a un punto di controllo dell'utilità esistente, è necessario disporre delle credenziali di amministratore o essere membro del ruolo Utility Reader. Si noti che può esistere un solo punto di controllo dell'utilità per Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed è possibile essere connessi a un solo punto di controllo dell'utilità da un'istanza di SSMS.  
  
 **Creare un nuovo** punto di controllo dell'utilità: per creare un nuovo punto di ![ ](../../database-engine/media/create-ucp.gif "Create_UCP")controllo dell'utilità, fare clic sul pulsante **Crea** punto di controllo dell'utilità nella parte superiore del riquadro Esplora utilità. Per creare un nuovo punto di controllo dell'utilità, è necessario specificare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fornire le credenziali di amministratore nella finestra di dialogo della connessione. Si tenga presente che per ogni istanza di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può esistere un solo punto di controllo dell'utilità.  
  
##  <a name="Instance_name"></a> Specifica istanza  
 Specificare le informazioni seguenti sul punto di controllo dell'utilità che si desidera creare:  
  
-   **Nome istanza** : per selezionare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dalla finestra di dialogo di connessione, fare clic su **Connetti.** Specificare il nome del computer e il nome dell'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel formato Nomecomputer\nomeistanza.  
  
-   **Nome utilità** : consente di specificare un nome che sarà utilizzato per identificare Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in rete.  
  
 Scegliere **Avanti**per continuare.  
  
##  <a name="Connection_dialog"></a> Finestra di dialogo della connessione  
 Nella finestra di dialogo Connetti al server, verificare il tipo di server, il nome del computer e il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Connetti al server &#40;Motore di database&#41;](../../ssms/f1-help/connect-to-server-database-engine.md).  
  
> [!NOTE]  
>  Se la connessione è crittografata, verrà utilizzata tale connessione. Se la connessione non è crittografata, Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si riconnetterà utilizzando una connessione crittografata.  
  
 Per continuare, fare clic su **Connetti**.  
  
##  <a name="Agent_configuration"></a> Account set di raccolta utilità  
 Specificare un account di dominio di Windows per eseguire il set di raccolta di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questo account viene utilizzato come account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per il set di raccolta di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In alternativa, è possibile utilizzare l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esistente. Per soddisfare i requisiti della convalida, utilizzare le linee guida seguenti per specificare l'account.  
  
 Se si specifica l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent:  
  
-   L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere un account di dominio di Windows che non è un account incorporato come LocalSystem, NetworkService o LocalService.  
  
 Scegliere **Avanti**per continuare.  
  
##  <a name="Validation_rules"></a> Regole di convalida  
 In questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]le condizioni seguenti devono essere vere per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui verrà creato il punto di controllo dell'utilità:  
  
|Regola di convalida|Azione correttiva|  
|---------------------|-----------------------|  
|È necessario disporre dei privilegi di amministratore per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui sarà creato il punto di controllo dell'utilità.|Accedere con un account con privilegi di amministratore per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|La versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere 10.50 o successiva.|Specificare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diversa per ospitare il punto di controllo dell'utilità.|  
|L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere un'edizione supportata. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).|Specificare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diversa per ospitare il punto di controllo dell'utilità.|  
|L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non deve essere un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registrata con altri punti di controllo dell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Specificare un'istanza diversa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ospitare il punto di controllo dell'utilità o annullare la registrazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal punto di controllo dell'utilità dove è attualmente un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può ospitare già un punto di controllo dell'utilità.|Specificare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diversa per ospitare il punto di controllo dell'utilità.|  
|L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificata deve avere TCP/IP abilitato.|Abilitare TCP/IP per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]specificata.|  
|L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può includere un database denominato "sysutility_mdw".|L'operazione di creazione del punto di controllo dell'utilità creerà un data warehouse di gestione dell'utilità (UMDW) denominato "sysutility_mdw". Per eseguire questa operazione, è necessario che il nome non sia presente nel computer quando le regole di convalida vengono eseguite. Per continuare, è necessario rimuovere o rinominare qualsiasi database denominato "sysutility_mdw". Per altre informazioni sulle operazioni di ridenominazione, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).|  
|È necessario arrestare i set di raccolta nell'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Arrestare i set di raccolta preesistenti mentre viene creato il punto di controllo dell'utilità nell'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se l'agente di raccolta dati è disabilitato, abilitarlo, arrestare qualsiasi set di raccolta dati eseguito, quindi eseguire nuovamente le regole di convalida per l'operazione di creazione del punto di controllo dell'utilità.<br /><br /> Per abilitare l'agente di raccolta dati:<br /><br /> In Esplora oggetti espandere il nodo **Gestione** .<br /><br /> Fare clic con il pulsante destro del mouse su **Raccolta dati**, quindi scegliere **Abilita raccolta dati**.<br /><br /> Per arrestare un set di raccolta:<br /><br /> In Esplora oggetti espandere il nodo Gestione, espandere **Raccolta dati**, quindi **Set di raccolta dati di sistema**.<br /><br /> Fare clic con il pulsante destro del mouse sul set di raccolta che si vuole arrestare, quindi scegliere **Arrestare il set di raccolta dati**.<br /><br /> In una finestra di messaggio verrà visualizzato il risultato di questa azione, mentre un cerchio rosso sull'icona del set di raccolta indicherà che il set di raccolta è stato arrestato.|  
|È necessario avviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nell'istanza specificata. Se l'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario configurare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in modo che venga avviato manualmente. In caso contrario, il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere configurato in modo che venga avviato automaticamente.|Avviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se l'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , configurare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in modo che venga avviato manualmente. In caso contrario, configurare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in modo che venga avviato automaticamente.|  
|È necessario configurare correttamente WMI.|Per risolvere i problemi di configurazione WMI, vedere [Attività e funzionalità di Utilità SQL Server](../../database-engine/troubleshoot-the-sql-server-utility.md).|  
|L'account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non può essere un account incorporato, come Servizio di rete.|Se l'account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è un account incorporato, come Servizio di rete, assegnare nuovamente l'account a un account di dominio di Windows sysadmin.|  
|Se si seleziona l'opzione relativa all'account proxy, l'account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere un account di dominio di Windows valido.|Specificare un account di dominio di Windows valido. Per verificare che l'account sia valido, accedere all'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'account di dominio di Windows.|  
|Se si seleziona l'opzione relativa all'account del servizio, l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non può essere un account incorporato, come Servizio di rete.|Se l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è un account incorporato, come Servizio di rete, assegnare nuovamente l'account a un account di dominio di Windows.|  
|Se si seleziona l'opzione relativa all'account del servizio, l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere un account di dominio di Windows valido.|Specificare un account di dominio di Windows valido. Per verificare che l'account sia valido, accedere all'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'account di dominio di Windows.|  
  
 Se alcune condizioni hanno dato risultati negativi nella convalida, correggere i problemi rilevati, quindi fare clic su **Riesegui convalida** per verificare la configurazione del computer.  
  
 Per salvare il report di convalida, fare clic su **Salva report** , quindi specificare un percorso per il file.  
  
 Scegliere **Avanti**per continuare.  
  
##  <a name="Summary"></a> Riepilogo  
 Nella pagina di riepilogo vengono visualizzate le informazioni fornite sul punto di controllo dell'utilità:  
  
-   Il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospita il punto di controllo dell'utilità.  
  
-   Il nome dell'istanza di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Il nome dell'account utente che verrà utilizzato per eseguire i processi per la raccolta dei dati di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per modificare le impostazioni di configurazione del punto di controllo dell'utilità, fare clic su **Indietro**. Scegliere **Avanti**per continuare.  
  
##  <a name="Creating_UCP"></a> Creazione del punto di controllo dell'utilità  
 Durante l'operazione per la creazione del punto di controllo dell'utilità, nella procedura guidata verranno visualizzati i passaggi e lo stato:  
  
-   Preparazione dell'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la creazione del punto di controllo dell'utilità.  
  
-   Creazione del data warehouse di gestione dell'utilità.  
  
-   Inizializzazione dell'UMDW di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; il nome del file UMDW è sysutility_mdw.  
  
-   Configurazione del punto di controllo dell'utilità.  
  
-   Configurazione del set di raccolta di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per salvare un report sull'operazione di creazione del punto di controllo dell'utilità, fare clic su **Salva report** , quindi specificare un percorso per il file.  
  
 Per completare la procedura guidata, fare clic su **Fine**.  
  
 Dopo aver completato la procedura guidata per la creazione del punto di controllo dell'utilità, nel riquadro di navigazione Esplora utilità in SSMS viene visualizzato un nodo per il punto di controllo dell'utilità al di sotto del quale sono presenti i nodi Applicazioni del livello dati distribuite, Istanze gestite e Amministrazione utilità. Il punto di controllo dell'utilità diventa automaticamente un'istanza gestita.  
  
 Il processo di raccolta dati inizia immediatamente, ma possono essere necessari fino a 30 minuti affinché i dati vengano visualizzati nel dashboard e i punti di visualizzazione nel riquadro del contenuto Esplora utilità. La raccolta dati continua una volta ogni 15 minuti. I dati iniziali proverranno dal punto di controllo dell'utilità stesso. Il punto di controllo dell'utilità è pertanto la prima istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per visualizzare il dashboard, fare clic su **Visualizza** , selezionare quindi **Contenuto Esplora utilità** nel menu SSMS. Per aggiornare i dati, fare clic con il pulsante destro del mouse sul nome dell'utilità nel riquadro Esplora utilità e scegliere **Aggiorna**.  
  
 Per altre informazioni su come registrare istanze aggiuntive di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Registrare un'istanza di SQL Server &#40;Utilità SQL Server&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md). Per rimuovere il punto di controllo dell'utilità come istanza gestita da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selezionare **Istanze gestite** nel riquadro **Esplora utilità** per popolare la visualizzazione elenco di istanze gestite, fare clic con il pulsante destro del mouse sul nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella visualizzazione elenco **Contenuto Esplora utilità** , quindi scegliere **Rendi istanza non gestita**.  
  
##  <a name="PowerShell_create_UCP"></a> Creazione di un nuovo punto di controllo dell'utilità utilizzando PowerShell  
 Utilizzare l'esempio seguente per creare un nuovo punto di controllo dell'utilità:  
  
```powershell
$UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
$SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
$Utility = [Microsoft.SqlServer.Management.Utility.Utility]::CreateUtility("Utility", $SqlStoreConnection, "ProxyAccount", "ProxyAccountPassword");  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e funzionalità di Utilità SQL Server](sql-server-utility-features-and-tasks.md)   
 [Risoluzione dei problemi relativi a Utilità SQL Server](../../database-engine/troubleshoot-the-sql-server-utility.md)  
