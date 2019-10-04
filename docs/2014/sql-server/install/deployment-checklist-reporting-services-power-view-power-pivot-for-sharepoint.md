---
title: 'Elenco di controllo per la distribuzione: Reporting Services, Power View e PowerPivot per SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9a2575c8-06fc-4ef4-9f24-c19e52b1bbcf
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f1eb0f6892192e5ed328386e6730ec3b1c41f05b
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952549"
---
# <a name="deployment-checklist-reporting-services-power-view-and-powerpivot-for-sharepoint"></a>Elenco di controllo per la distribuzione: Reporting Services, Power View e PowerPivot per SharePoint
  Usare il seguente elenco di controllo per installare queste funzionalità di business intelligence nella stessa farm di SharePoint: PowerPivot per SharePoint, Generatore report e [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. Sebbene nell'elenco di controllo venga consigliato un ordine di installazione specifico, in pratica è possibile installare queste funzionalità pressoché in qualsiasi ordine. Nell'elenco di controllo si suppone che i seguenti prodotti e funzionalità siano installati:  
  
1.  SharePoint Server 2010 con Service Pack 1 (SP1)  
  
2.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] motore di database  
  
3.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services e componente aggiuntivo di Reporting Services  
  
4.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot per SharePoint  
  
 Una volta installate queste funzionalità, sarà possibile effettuare le operazioni indicate di seguito.  
  
-   Accedere alle cartelle di lavoro di PowerPivot create in PowerPivot per Excel dai siti di SharePoint.  
  
-   Compilare report [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] interattivi basati sulle cartelle di lavoro di PowerPivot in SharePoint.  
  
-   Compilare report di Generatore report all'avvio di Generatore report in SharePoint.  
  
> [!NOTE]  
>  Per PowerPivot per SharePoint è richiesta l'installazione di SharePoint 2010 Service Pack 1 (SP1) nella farm di SharePoint. Se si installa il software a scopo di valutazione, è consigliabile iniziare utilizzando un server pulito in modo da evitare l'overhead richiesto per l'aggiornamento di una farm. L'aggiornamento di una farm ha ripercussioni sulle operazioni di SharePoint e in genere richiede un'attenta pianificazione. Per installare PowerPivot per SharePoint il più rapidamente possibile, seguire questo approccio: installare SharePoint 2010, installare SharePoint 2010 SP1, quindi configurare la farm in un passaggio successivo. L'aggiornamento viene evitato perché non è configurata la farm ancora quando si installa SharePoint 2010 SP1.  
>   
>  In questo elenco di controllo, il passaggio della configurazione della farm è presupposto durante la configurazione di PowerPivot per SharePoint, l'utilizzo dello Strumento di configurazione PowerPivot. Per un approccio alternativo, utilizzare la Configurazione guidata del prodotto SharePoint. Con entrambi gli approcci si ottiene una farm operativa che supporta PowerPivot per SharePoint.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire il programma di installazione di SQL Server, è necessario essere un amministratore locale.  
  
 SharePoint Server 2010 Enterprise Edition è richiesto per PowerPivot per SharePoint. È anche possibile usare l'edizione Enterprise di valutazione.  
  
 È necessario che SharePoint Server 2010 SP1 sia installato. In caso contrario, non è possibile configurare la farm per usare le funzionalità di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] .  
  
 Il computer deve fare parte di un dominio.  
  
 È necessario disporre di uno o più account utente di dominio per eseguire il provisioning dei servizi. Sono necessari account utente di dominio per i servizi seguenti: Servizi Web di SharePoint e servizi amministrativi, Reporting Services, Analysis Services, Excel Services, servizi di archiviazione sicura e Servizio di sistema PowerPivot. Gli account di dominio sono richiesti dalla funzionalità account gestiti in SharePoint. È possibile effettuare il provisioning del motore di database utilizzando un account virtuale, ma tutti gli altri servizi devono essere eseguiti come un utente di dominio.  
  
 È necessario disporre del nome di istanza di PowerPivot. Sul computer su cui si installa PowerPivot per SharePoint non deve essere presente un'istanza denominata di PowerPivot esistente.  
  
 Se si installa PowerPivot per SharePoint su una farm esistente, è necessario che una o più applicazioni Web SharePoint siano configurate per l'autenticazione in modalità classica. L'accesso ai dati PowerPivot funzionerà solo se l'applicazione Web supporta l'autenticazione in modalità classica. Per altre informazioni sui requisiti della modalità classica, vedere [PowerPivot Authentication and Authorization](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization).  
  
 Esaminare gli argomenti aggiuntivi seguenti per comprendere i requisiti relativi al sistema e alla versione:  
  
-   [Guida per l'utilizzo delle funzionalità di Business Intelligence di SQL Server in una farm di SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
## <a name="steps"></a>Passaggi  
 Nei seguenti passaggi si presuppone che l'installazione e la configurazione del server vengano eseguite da un amministratore. L'utente di installazione in SharePoint è anche un amministratore di farm e spesso anche l'amministratore principale della raccolta siti predefinita. Se i passaggi seguenti vengono suddivisi tra più persone, potrebbero essere richieste autorizzazioni aggiuntive per garantirne il corretto funzionamento.  
  
|Passaggio|Collegamento|  
|----------|----------|  
|Eseguire l'Utilità preparazione prodotti SharePoint 2010.|È necessario disporre dei supporti di installazione di SharePoint 2010. L'utilità di preparazione corrisponde al file PrerequisiteInstaller.exe disponibile nei supporti di installazione.|  
|Installare SharePoint Server 2010 Enterprise Edition oppure l'edizione Enterprise Evaluation.|Quando si installa SharePoint, è possibile scegliere di configurare la farm successivamente, non eseguendo la Configurazione guidata Prodotti SharePoint 2010 al termine dell'installazione. In attesa di configurare la farm, sarà possibile utilizzare un'istanza di motore di database [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], che verrà installata in un passaggio successivo, come server di database della farm. Per configurare la farm, si utilizzerà lo strumento di configurazione PowerPivot. Sono incluse azioni per eseguire il provisioning della farm se la farm non è ancora configurata.|  
|Installare SharePoint Server 2010 SP1.|Scaricare SP1 da [https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697).|  
|Eseguire il programma di installazione di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] per installare il motore di database e PowerPivot per SharePoint.|[Installare PowerPivot per SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> Nel passaggio 1 viene descritta la procedura di installazione di PowerPivot per SharePoint. Durante questo passaggio, assicurarsi di selezionare la casella di controllo per l'aggiunta del motore di database al ruolo nella pagina Impostazione ruolo. In questo modo, l'motore di database viene aggiunta all'installazione in modo che sia possibile utilizzarla come server di database della farm quando si configura la farm nel passaggio successivo. Se la farm è già configurata, tuttavia, è possibile ignorare questo passaggio.<br /><br /> Nel passaggio 2 viene richiesto di configurare il server. Per questo passaggio, scegliere lo strumento di configurazione PowerPivot. Sebbene siano disponibili diversi approcci, l'utilizzo dello strumento di configurazione rappresenta il metodo più efficiente per un'installazione autonoma.<br /><br /> Se SharePoint 2010 è installato ma non configurato, nello strumento vengono preselezionate le azioni per creare la farm, un'applicazione Web predefinita e una raccolta di siti radice. Assicurarsi di lasciare queste opzioni selezionate in modo che la farm venga creata. Se la farm è già stata configurata, queste azioni vengono omesse nello strumento, dove risultano disponibili solo le opzioni necessarie per la configurazione di PowerPivot per SharePoint.<br /><br /> Nel passaggio 3 viene illustrata la procedura di installazione della versione SQL Server 2008 R2 del provider OLE DB per Analysis Services. Questo passaggio è fondamentale per il supporto delle versioni di cartelle di lavoro create con la versione 2008 R2 di PowerPivot per Excel.|  
|Verificare che la farm sia operativa.|Innanzitutto, avviare Amministrazione centrale e verificare che sia disponibile. Aprire quindi il sito del team immettendo http://localhost.  Viene visualizzato il sito del team SharePoint.|  
|Verificare che PowerPivot per SharePoint sia operativo.|[Verificare un'installazione di PowerPivot per SharePoint](https://docs.microsoft.com/analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation)<br /><br /> Questa attività conferma l'accesso ai dati PowerPivot utilizzando una cartella di lavoro di esempio da caricare.|  
|Eseguire il programma di installazione di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] per installare e configurare Reporting Services e il componente aggiuntivo di Reporting Services.|[Installare la modalità SharePoint di Reporting Services per SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)<br /><br /> Facoltativamente, durante l'installazione di Reporting Services, è possibile aggiungere un'altra istanza di Analysis Services all'albero delle funzionalità del programma di installazione per avere a disposizione una seconda risorsa per ospitare i dati tabulari. L'istanza aggiuntiva di Analysis Services verrebbe utilizzata per ospitare i database modello tabulare creati in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. I database tabulari rappresentano una valida origine dati per i report [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .<br /><br /> [Installare Analysis Services in modalità Tabella](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)|  
|Verificare che Reporting Services sia operativo.|[Verificare un'installazione di Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)|  
|(Amministratori del sito) Configurare le autorizzazioni di SharePoint.|Per aggiungere, modificare o eliminare elementi nelle raccolte di SharePoint sono richieste le autorizzazioni di collaborazione. Il livello di autorizzazione di visualizzazione è sufficiente per l'accesso in sola lettura ai report e alle cartelle di lavoro di PowerPivot con dati incorporati.<br /><br /> Le cartelle di lavoro di PowerPivot a cui si accede come origini dati esterne (dove l'URL della cartella di lavoro è una stringa di connessione in un'altra cartella di lavoro o in un altro report) richiedono autorizzazioni di lettura, che sono superiori alle autorizzazioni di visualizzazione.<br /><br /> Anche per le connessioni BISM sono richieste autorizzazioni di lettura. Potrebbe essere necessario creare nuovi livelli di autorizzazione o gruppi di SharePoint per rendere disponibili le autorizzazioni corrette.|  
|(Amministratori del sito) Estendere le raccolte documenti|Estendere le raccolte documenti per usare i tipi di contenuto BI: Connessioni BI Semantic Model, Reporting Services origini dati condivise Generatore report report:<br /><br /> 1) <br />                    **Abilitare la gestione dei tipi di contenuto**. Nella scheda Libreria di Documenti condivisi fare clic su **Impostazioni raccolta**. Fare clic su **Impostazioni avanzate**in Impostazioni generali. In Tipi di contenuto selezionare **Sì** per consentire la gestione dei tipi di contenuto, quindi fare clic su **OK**.<br /><br /> 2) <br />                    **Selezionare i tipi di contenuto di Business Intelligence**. Nella scheda LIbreria scegliere **Impostazioni raccolta**. In Tipi di contenuto fare clic su **Aggiungi da tipi di contenuto del sito esistenti**. Dal gruppo dei tipi di contenuto di Business Intelligence aggiungere **File di connessione BISM** e **Origini dei dati del report**. Facoltativamente, è possibile aggiungere anche altri tipi di contenuto di Reporting Services, ad esempio Modello di report, per abilitare scenari di compilazione di report aggiuntivi.<br /><br /> <br /><br /> Per ulteriori informazioni, vedere [aggiungere un tipo di contenuto connessione BI Semantic Model a una &#40;raccolta&#41; PowerPivot per SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library) e [aggiungere tipi di contenuto del server di &#40;report a una raccolta Reporting Services in modalità&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).|  
|(Amministratori del sito) Creare i file di connessione dati utilizzati per avviare [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].|È necessario creare una connessione BISM (con estensione bism) o un'origine dei dati condivisa di Reporting Services (con estensione rsds) come origine dati per [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. Dopo avere creato un file di connessione dati, è possibile avviare [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] utilizzando la connessione dati come origine dati.<br /><br /> [Creare una connessione BISM (BI Semantic Model) a una cartella di lavoro di PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook)<br /><br /> [Creare una connessione BISM a un database modello tabulare](../../relational-databases/databases/model-database.md)<br /><br /> Nota: [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] è disponibile perché è stata installata la versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] di Reporting Services e il server è stato configurato come servizio condiviso. Se Reporting Services è stato installato e configurato per il livello di integrazione SQL Server 2008, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] non è disponibile.|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità supportate dalle edizioni di SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)  
  
  
