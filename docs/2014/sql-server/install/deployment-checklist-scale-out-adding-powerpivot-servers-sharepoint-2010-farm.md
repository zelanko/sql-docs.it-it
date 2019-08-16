---
title: "Elenco di controllo per la distribuzione: Scalabilità orizzontale mediante l'aggiunta di server PowerPivot a una farm di SharePoint 2010 | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2dbddcc7-427a-4537-a8e2-56d99b9d967d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: db17c7d395507072745ec8c4b7dd606efea75230
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/16/2019
ms.locfileid: "69530932"
---
# <a name="deployment-checklist-scale-out-by-adding-powerpivot-servers-to-a-sharepoint-2010-farm"></a>Elenco di controllo per la distribuzione: Scalabilità orizzontale tramite aggiunta di server PowerPivot a una farm di SharePoint 2010
  Se si prevede un volume elevato di richieste per l'elaborazione di query PowerPivot in una farm di SharePoint, è possibile aggiungere un'ulteriore istanza di PowerPivot per SharePoint per supportare in modo facile l'elaborazione di query e dati.  
  
 Dopo aver installato una nuova istanza, si dispone di capacità aggiuntive per l'esecuzione di query sui dati PowerPivot o l'elaborazione di processi di aggiornamento dati PowerPivot. Facoltativamente, è possibile configurare ogni server per gestire un solo tipo di richiesta: query o aggiornamento dati.  
  
## <a name="prerequisites"></a>Prerequisiti  
 SharePoint Server 2010 è installato e configurato.  
  
 SharePoint Server 2010 SP1 è applicato e la farm è aggiornata.  
  
 L'istanza di PowerPivot per SharePoint esistente nella farm è [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], ovvero una nuova installazione o un aggiornamento da SQL Server 2008 R2.  
  
 Il computer su cui viene installato il nuovo server [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot per SharePoint viene unito in join alla farm. Il computer e gli altri server nella farm devono appartenere allo stesso dominio.  
  
 Esaminare gli argomenti aggiuntivi seguenti per comprendere i requisiti relativi al sistema e alla versione:  
  
-   [Guida per l'utilizzo delle funzionalità di Business Intelligence di SQL Server in una farm di SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
> [!NOTE]  
>  In una farm con più server, la versione di tutte le istanze di PowerPivot per SharePoint deve essere identica. Se sono stati applicati Service Pack o aggiornamenti ad altri server PowerPivot già presenti nella farm, la nuova istanza che si intende aggiungere dovrà essere aggiornata alla stessa versione dell'istanza esistente già presente nella farm. La nuova istanza non sarà disponibile finché gli aggiornamenti non sono stati applicati.  
  
## <a name="steps"></a>Passaggi  
 Utilizzare l'elenco di controllo in questo argomento per aggiungere altri server PowerPivot a una farm SharePoint. Queste istruzioni presuppongono che si disponga già di un server PowerPivot per SharePoint nella farm e che si intenda aggiungere un secondo server per gestire un carico di elaborazione aggiuntivo. Fatta eccezione per le differenze nei requisiti di installazione, nella configurazione dopo l'installazione e nella verifica, i passaggi per la distribuzione di una soluzione con scalabilità orizzontale sono identici a quelli per l'aggiunta di un singolo server PowerPivot a una farm esistente.  
  
|Passaggio|Collegamento|  
|----------|----------|  
|Determinare l'account del servizio dell'istanza di Analysis Services già presente nella farm|Ogni istanza aggiuntiva installata deve essere eseguita nello stesso account della prima istanza. Utilizzare uno degli approcci per determinare l'account del servizio:<br /><br /> Nella sezione sicurezza di amministrazione centrale fare clic su **Configura account di servizio**. Selezionare **servizio Windows-SQL Server Analysis Services**. Dopo aver selezionato il servizio, il nome dell'account del servizio verrà visualizzato nella pagina.<br /><br /> In un server che dispone già di un'installazione del servizio PowerPivot, aprire l'applicazione console **Servizi** in strumenti di amministrazione. Fare doppio clic su **SQL Server Analysis Services**. Fare clic sulla scheda **accesso** per visualizzare l'account del servizio.<br />**Importante utilizzaresolo\* amministrazione centrale per modificare gli account del servizio. \* \* \*** Se si utilizza un altro strumento o un approccio diverso, le autorizzazioni non verranno aggiornate correttamente nella farm.|  
|Eseguire il programma di installazione per installare una seconda istanza di PowerPivot per SharePoint.|[Installare PowerPivot per SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> Scegliere un server applicazioni che viene unito in join alla farm, ma che non dispone di un'istanza PowerPivot esistente sul server.<br /><br /> Durante l'installazione, quando viene richiesto di specificare un account, immettere l'account specificato nel passaggio precedente. Tutte le istanze del servizio Analysis Services devono essere eseguite nello stesso dominio. Questo requisito abilita l'utilizzo della funzionalità account gestiti in SharePoint che consente di aggiornare la password in un'unica posizione per tutte le istanze del servizio dello stesso tipo.|  
|Configurare la seconda istanza|Per configurare l'istanza di, è possibile utilizzare uno dei due approcci seguenti: [Powerpivot strumenti di configurazione](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools) o [configurazione PowerPivot con Windows PowerShell](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)<br /><br /> Quando si configura una seconda istanza, è necessario solo effettuare il provisioning dei servizi locali. Tutte le altre attività di configurazione (ad esempio, la creazione di applicazioni di servizio o la configurazione dell'aggiornamento dati) vengono eseguite durante la configurazione iniziale e utilizzate dalle istanze successive installate.|  
|Attività successive all'installazione|Non sono richiesti ulteriori passaggi. Non è necessario creare applicazioni di servizio, attivare funzioni, distribuire soluzioni o modificare l'identità dell'applicazione di servizio. Il nuovo software server verrà individuato e utilizzato automaticamente dalle applicazioni di servizio e dalle applicazioni Web esistenti.<br /><br /> Facoltativamente, se è stato installato un secondo server al fine di utilizzare un server per le query e uno per l'aggiornamento dati, è possibile configurare le proprietà dell'istanza del server ora per specificare il tipo di richieste gestite da ogni server. Per altre informazioni, vedere [configurare l'aggiornamento dati dedicato o l'elaborazione &#40;solo query&#41;PowerPivot per SharePoint](../../analysis-services/configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md).|  
|Verificare l'installazione della seconda istanza|È possibile utilizzare i passaggi seguenti per verificare l'elaborazione di query PowerPivot nel server appena installato.<br /><br /> 1) in Amministrazione centrale aprire la pagina Gestisci servizi nel server per verificare che il server e i relativi servizi siano visualizzati.<br />-In server fare clic sulla freccia verso il basso, fare clic su Cambia server, quindi selezionare il server con la nuova installazione di PowerPivot per SharePoint.<br />-Verificare che SQL Server Analysis Services e SQL Server Servizio di sistema PowerPivot siano avviati.<br /><br /> 2) in Amministrazione centrale arrestare gli altri server PowerPivot per SharePoint in modo che il server appena installato sia l'unico disponibile. Per ulteriori informazioni, vedere [avviare o arrestare un Server PowerPivot per SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server).<br /><br /> 3) fare clic su una cartella di lavoro di PowerPivot per aprirla dalla libreria.<br /><br /> 4) fare clic su un filtro dei dati o trasformare i dati tramite pivot per avviare una query. I dati PowerPivot verranno caricati in background. Nel passaggio successivo verrà effettuata la connessione al server per verificare che i dati vengano caricati e memorizzati nella cache.<br /><br /> 5) avviare SQL Server Management Studio dal gruppo di programmi Microsoft SQL Server nel menu Start. Se questo strumento non è installato nel server, è possibile ignorare l'ultimo passaggio per confermare la presenza di file memorizzati nella cache.<br /><br /> 6) in tipo di server selezionare **Analysis Services**.<br /><br /> 7) in nome server immettere  **\<nome-server > \powerpivot**, dove  **\<Server-Name >** è il nome del computer in cui è presente il nuovo PowerPivot per SharePoint installazione.<br /><br /> 8) fare clic su **Connetti**.<br /><br /> 9) in Esplora oggetti fare clic su **database** per visualizzare l'elenco dei file di dati PowerPivot caricati.<br /><br /> 10) nel computer file system, controllare la cartella seguente per determinare se i file vengono memorizzati nella cache su disco. La presenza di file memorizzati nella cache è un'ulteriore verifica che la distribuzione è operativa. Per visualizzare la cache dei file, spostarsi nella cartella \Programmi\Microsoft SQL Server\MSAS11.POWERPIVOT\OLAP\Backup.<br /><br /> 11) riavviare i servizi arrestati in precedenza.|  
  
## <a name="see-also"></a>Vedere anche  
 [PowerPivot per SharePoint di &#40;configurazione iniziale&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [Installazione di PowerPivot per SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Amministrazione e configurazione del server PowerPivot in Amministrazione centrale](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)  
  
  
