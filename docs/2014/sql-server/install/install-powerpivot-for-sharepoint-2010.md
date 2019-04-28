---
title: Installare PowerPivot per SharePoint 2010 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: eec38696-5e26-46fa-bc83-aa776f470ce8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e02b80c1967059f91e3a97fb940a2715c6beebb8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62656771"
---
# <a name="install-powerpivot-for-sharepoint-2010"></a>Installare PowerPivot per SharePoint 2010
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] è una raccolta di servizi di livello intermedio e di back-end che forniscono l'accesso ai dati PowerPivot in una farm di SharePoint 2010. Se l'organizzazione utilizza l'applicazione client, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel 2010, per creare cartelle di lavoro che contengono dati analitici, è necessario disporre di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] per accedere a tali dati in un ambiente server. In questo argomento viene illustrato il processo di installazione di base e vengono forniti collegamenti ad argomenti aggiuntivi di supporto alla configurazione di PowerPivot.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
 
  
 Per istruzioni su come installare [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sullo stesso server, vedere [elenco di controllo distribuzione: Reporting Services, Power View e PowerPivot per SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md).  
  
## <a name="prerequisites"></a>Prerequisiti  
  
1.  Per eseguire il programma di installazione di SQL Server, è necessario essere un amministratore locale.  
  
2.  È richiesta l'edizione SharePoint Server 2010 Enterprise per [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. È anche possibile usare l'edizione Enterprise di valutazione.  
  
3.  È necessario che SharePoint Server 2010 SP2 sia installato. In caso contrario, non è possibile configurare la farm per usare le funzionalità di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
4.  Il computer deve fare parte di un dominio.  
  
5.  È necessario disporre di un account utente di dominio per eseguire il provisioning di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. In un'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], l'account del servizio Analysis Services deve essere un account utente di dominio in modo da poterlo gestire da Amministrazione centrale. Si digiterà l'account e credenziali sul **configurazione Server** pagina come parte della procedura in questo documento.  
  
6.  È necessario disporre del nome di istanza di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Sul computer su cui si installa PowerPivot per SharePoint non deve essere presente un'istanza denominata di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] esistente.  
  
7.  Un'istanza di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] non può far parte di un cluster di failover di SQL Server. Utilizzare le funzionalità di disponibilità elevata del prodotto SharePoint. Ad esempio, Excel Services gestisce il bilanciamento del carico dei server PowerPivot per SharePoint. Per altre informazioni, vedere [impostazioni (SharePoint Server 2013) del modello di dati di gestire Excel Services](https://technet.microsoft.com/library/jj219780.aspx) (https://technet.microsoft.com/library/jj219780.aspx).  
  
8.  Se si installa [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] su una farm esistente, è necessario che una o più applicazioni Web SharePoint siano configurate per l'autenticazione in modalità classica. L'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] funzionerà solo se l'applicazione Web supporta l'autenticazione in modalità classica. Per altre informazioni sui requisiti della modalità classica, vedere [PowerPivot Authentication and Authorization](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md).  
  
9. Esaminare gli argomenti aggiuntivi seguenti per comprendere i requisiti relativi al sistema e alla versione:  
  
    -   [Guida per l'utilizzo delle funzionalità di Business Intelligence di SQL Server in una farm di SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="InstallSQL"></a> Passaggio 1: Installare PowerPivot per SharePoint  
 In questo passaggio viene eseguito il programma di installazione di SQL Server per installare [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. In un passaggio successivo, il server verrà configurato come attività successiva all'installazione.  
  
1.  Inserire i supporti di installazione o aprire una cartella che contiene i file di installazione per SQL Server e quindi fare doppio clic su **setup.exe**.  
  
2.  Fare clic su **installazione** nel riquadro di spostamento a sinistra.  
  
3.  Fare clic su **Nuova installazione autonoma di SQL Server o aggiunta di funzionalità a un'installazione esistente**.  
  
4.  Nel **codice Product Key** pagina specificare l'edizione evaluation o immettere un codice product key per una copia concessa in licenza della enterprise edition.  
  
     Scegliere **Avanti**.  
  
5.  Accettare le condizioni di licenza software Microsoft. Inoltre, si apprezza se si abilitano anche l'Analisi utilizzo software e la segnalazione errori. Scegliere **Avanti**.  
  
6.  Se richiesto, aggiornare i file di installazione.  
  
7.  Nel **regole di installazione** pagina, il programma di installazione riportati i problemi che potrebbero impedire l'installazione. Esaminare l'elenco per determinare se sono stati individuati problemi potenziali nel sistema.  
  
    > [!NOTE]  
    >  Dal momento che Windows Firewall è abilitato, verrà richiesto di aprire le porte per abilitare l'accesso remoto. Generalmente, questo avviso non è applicabile alle installazioni di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Le connessioni ai servizi e ai file di dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] vengono effettuate utilizzando le porte di SharePoint già aperte per la comunicazione da servizio a servizio di SharePoint.  
  
     Scegliere **Avanti**. Attendere che i file del programma di installazione di SQL Server vengono installati nel server.  
  
8.  Nella pagina **Impostazione ruolo** selezionare **SQL Server PowerPivot per SharePoint**.  
  
9. Facoltativamente, è possibile aggiungere un'istanza del Motore di database all'installazione. È possibile eseguire questa operazione se si sta configurando una nuova farm ed è necessario un server di database per eseguire i database di configurazione e il contenuto della farm. Il motore di database eventualmente aggiunto, verrà installato come un'istanza denominata PowerPivot. Ogni volta che è necessario specificare una connessione a questa istanza (ad esempio, nella configurazione guidata farm se si utilizza tale procedura guidata per configurare la farm), immettere il nome del database nel formato seguente: <`servername`> \powerpivot.  
  
     ![GMNI_SetupUI_FeatureRole](../../../2014/sql-server/install/media/gmni-setupui-featurerole.gif "GMNI_SetupUI_FeatureRole")  
  
10. Scegliere **Avanti**.  
  
11. Nel **Selezione funzionalità** viene visualizzata la pagina, un elenco di sola lettura delle funzionalità che verrà installato a scopo informativo. Non è possibile aggiungere o rimuovere elementi preselezionati per questo ruolo. Scegliere **Avanti**.  
  
12. Nel **regole di funzionalità** pagina, fare clic su **successivo**. La pagina può essere ignorata.  
  
13. Nella pagina **Configurazione dell'istanza** un nome dell'istanza in sola lettura di "PowerPivot" viene visualizzato a scopo informativo. Questo nome dell'istanza **POWERPIVOT** viene **obbligatorio e non può essere modificato**. È tuttavia possibile immettere un ID istanza univoco per specificare un nome di directory descrittivo e chiavi del Registro di sistema. Scegliere **Avanti**.  
  
14. Nel **configurazione Server** , digitare le informazioni sull'account desiderato.  
  
     Per SQL Server Analysis Services, è necessario specificare un account utente di dominio. Non specificare un account predefinito. Gli account di dominio sono obbligatori per la gestione di account del servizio Analysis Services come un *account gestito* in Amministrazione centrale SharePoint.  
  
     ![Configurazione del Server SSAS](../../../2014/sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "configurazione del Server SSAS")  
  
     Se si aggiungono il Motore di database di SQL Server e SQL Server Agent, è possibile configurare i servizi da eseguire in account utente di dominio o in account virtuali predefiniti.  
  
     Non usare mai il proprio account utente di dominio per eseguire il provisioning di un servizio. Con questa operazione si concedono al server le stesse autorizzazioni di cui l'utente dispone per le risorse disponibili nella rete. Se un utente malintenzionato compromette il server, potrà accedere con le credenziali di dominio dell'utente valido e scaricare o usare gli stessi dati e applicazioni.  
  
15. Scegliere **Avanti**.  
  
16. Se si installa il motore di database, viene visualizzata la pagina relativa alla configurazione del motore di database. Nella configurazione del motore di Database, fare clic su **Aggiungi utente corrente** per concedere all'utente le autorizzazioni di amministratore account per l'istanza del motore di Database. Fare clic su **Add** per aggiungere altri account. Scegliere **Avanti**.  
  
17. Nella pagina **Configurazione di Analysis Services** fare clic su **Aggiungi utente corrente** per concedere le autorizzazioni amministrative dell'account utente. Saranno necessarie autorizzazioni amministrative per configurare il server dopo che è stata completata l'installazione.  
  
18. Nella stessa pagina aggiungere l'account utente di Windows di qualsiasi altra persona che richiede autorizzazioni amministrative. Ad esempio, qualsiasi utente che desidera connettersi all'istanza del [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] in SQL Server Management Studio per risolvere problemi di connessione al database o ottenere informazioni sulla versione deve disporre di autorizzazioni di amministratore di sistema per il server. Aggiungere l'account utente di qualsiasi persona che potrebbe avere la necessità di risolvere problemi o amministrare il server.  
  
19. Scegliere **Avanti**.  
  
20. Fare clic su **successivo** su tutte le pagine rimanenti finché non viene visualizzata la pagina Inizio installazione.  
  
21. Fare clic su **Installa**.  
  
> [!TIP]  
>  Se è necessario risolvere i problemi relativi l'installazione di SQL Server, vedere [visualizzare e leggere i file Log di SQL Server Setup](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
##  <a name="bkmk_config"></a> Passaggio 2: Configurare il Server  
  
> [!IMPORTANT]  
>  Prima di configurare [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] o una farm di SharePoint che utilizza un server di database [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] è necessario che SharePoint 2010 SP2 sia installato. Se non è stato ancora installato un Service Pack, eseguire adesso questa operazione prima di iniziare a configurare il server.  
  
 L'Installazione non è completa fino a che non viene configurato il server. In questa versione, configurazione del server viene sempre eseguita come attività di post-installazione, utilizzando uno degli approcci seguenti: [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Lo strumento di configurazione, amministrazione centrale o PowerShell. Per continuare, scegliere uno degli approcci seguenti:  
  
-   [Configurare o ripristinare PowerPivot per SharePoint 2010 &#40;strumento di configurazione PowerPivot&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)  
  
-   [Amministrazione e configurazione del server PowerPivot in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
-   [Configurazione di PowerPivot tramite Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
 **La connessione all'istanza del motore di Database.** Dopo l'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], è possibile aggiungere un'istanza del motore di database all'installazione mediante il programma di installazione di SQL Server. Potrebbe essere aggiunta un'istanza del motore di Database all'installazione se si sta configurando una nuova farm ed è necessario un server di database per eseguire i database del contenuto e la configurazione della farm. Se il motore di database è stato aggiunto, è stato installato come un'istanza denominata di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Ogni volta che è necessario specificare una connessione a questa istanza (ad esempio, nella configurazione guidata farm se si utilizza tale procedura guidata per configurare la farm), ricordare di immettere il nome del database nel formato: <`servername`> \powerpivot.  
  
##  <a name="bkmk_redist"></a> Passaggio 3: Installare i provider OLE DB per Analysis Services nei server dell'applicazione Excel Services  
 Se i servizi di calcolo Excel e [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] vengono eseguiti in server applicazioni diversi, sono necessari ulteriori passaggi di installazione. Nei server applicazioni in cui vengono eseguiti i servizi di calcolo Excel installare la versione appropriata del provider OLE DB (MSOLAP) di Analysis Services.  
  
-   La versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di MSOLAP è inclusa nel programma di installazione di SQL Server, pertanto l'installazione esplicita della versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di MSOLAP è necessaria solo se il server applicazioni non è PowerPivot.  
  
    > [!NOTE]  
    >  Il server applicazioni di servizi di calcolo Excel è inoltre richiesta un'istanza del file **Microsoft.AnalysisServices.Xmla.dll** nell'assembly globale. Per installare il file con estensione dll nel server applicazioni, installare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Selezionare il "strumenti di gestione - completa" nel **Selezione funzionalità** pagina della procedura guidata il programma di installazione di SQL Server.  
  
-   Se si desidera che il server applicazioni supporti le cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] precedenti, è necessario installare la versione SQL Server 2008 R2 di MSOLAP.  
  
 Per altre informazioni sull'installazione del provider, inclusi i passaggi di verifica, vedere [installare il Provider OLE DB di Analysis Services nei server SharePoint](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
##  <a name="bkmk_verify"></a> Passaggio 4: Verificare l'installazione  
 In quest'ultimo passaggio, si verificherà la completa funzionalità di SharePoint 2010 e di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Per istruzioni, vedere [Verify a PowerPivot for SharePoint Installation](../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione PowerPivot per SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Elenco di controllo di distribuzione: Reporting Services, Power View e PowerPivot per SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)   
 [Elenco di controllo di distribuzione: Scalabilità orizzontale aggiungendo server PowerPivot a una farm di SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)   
 [Elenco di controllo di distribuzione: Installazione MultiServer di PowerPivot per SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-multiserver-installation-powerpivot-sharepoint-2010.md)  
  
  
