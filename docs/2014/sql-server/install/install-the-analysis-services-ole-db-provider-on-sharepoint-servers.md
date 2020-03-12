---
title: Installare il Provider OLE DB Analysis Services nei server SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2c62daf9-1f2d-4508-a497-af62360ee859
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 1146c612225c2f58dd501ce9cba658ca7ca6ba69
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112172"
---
# <a name="install-the-analysis-services-ole-db-provider-on-sharepoint-servers"></a>Installazione del provider OLE DB di Analysis Services nei server di SharePoint
  Il provider Microsoft OLE DB per Analysis Services (MSOLAP) è un'interfaccia utilizzata dalle applicazioni client per interagire con i dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Le richieste di connessione ai dati [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] vengono gestite dal provider in un ambiente di SharePoint in cui è installato [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
 Il provider di dati viene incluso nel pacchetto di installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] (spPowerPivot.msi), ma potrebbe richiedere l'installazione manuale. Vi sono due motivi per cui potrebbe essere necessario installare manualmente una libreria client o un provider di dati in un server SharePoint.  
  
-   **Abilita la compatibilità con le versioni precedenti**. Con le cartelle di lavoro [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] è possibile specificare la versione [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del provider OLE DB di Analysis Services nella relativa stringa di connessione. Di conseguenza, la versione di questo provider deve essere presente nel computer affinché la richiesta venga soddisfatta.  
  
-   **Abilitare l'accesso ai dati in un'istanza di Excel Services dedicata**. Se nella farm di SharePoint è incluso Excel Services in un server che non dispone di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], installare la versione [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] del provider e degli altri componenti di connettività client utilizzando il pacchetto di installazione [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
    > [!NOTE]  
    >  Queste scenari non si escludono a vicenda. Per l'hosting di versioni di cartelle di lavoro in una farm in cui sono inclusi server applicazioni che eseguono Excel Services senza un'istanza di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] sarà necessaria l'installazione delle versioni meno recenti e di quelle più recenti del provider di dati in ogni computer Excel Services.  
  
  
##  <a name="bkmk_vers"></a>Versioni del provider di OLE DB che supportano l'accesso ai dati PowerPivot  
 In una farm di SharePoint possono essere incluse più versioni del provider OLE DB per Analysis Services, anche le versioni precedenti che non supportano l'accesso ai dati PowerPivot.  
  
 Per impostazione predefinita, con SharePoint 2010 viene installata la versione [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] del provider. Anche se è identificata come MSOLAP.4 (stesso numero di versione utilizzato per [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]), questa versione non consente l'accesso ai dati PowerPivot. Per la riuscita delle connessioni, è necessario disporre della versione [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del provider.  
  
 Una versione successiva a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] del provider OLE DB include trasporti e supporto di connessione per le strutture dei dati di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Le cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] utilizzano le versioni più recenti di questo provider per richiedere l'elaborazione di query dai server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] della farm. Per ottenere una versione aggiornata, è possibile scaricarla e installarla tramite la pagina dei Feature Pack di SQL Server.  
  
 Nella tabella seguente vengono descritte le versioni valide.  
  
|Versione del prodotto|Versione file|Valida per:|  
|---------------------|------------------|----------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|MSOLAP100.dll nel file system<br /><br /> MSOLAP.4 in una stringa di connessione Excel<br /><br /> 10.50.1600 o successiva nei dettagli della versione del file|Utilizzare i modelli di dati creati con la versione [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] di PowerPivot per Excel.|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|MSOLAP110.dll nel file system<br /><br /> MSOLAP.5 in una stringa di connessione Excel<br /><br /> 11.0.0000 o successiva nei dettagli della versione del file|Utilizzare i modelli di dati creati con la versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel.|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|MSOLAP120.dll nel file system<br /><br /> 12.0.20000 o successiva nei dettagli della versione del file|Utilizzare per modelli di dati diversi dai modelli di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|  
  
  
##  <a name="bkmk_why"></a>Perché è necessario installare il provider di OLE DB  
 In due scenari è richiesta l'installazione manuale del provider OLE DB nei server della farm.  
  
 **Lo scenario più comune** si verifica quando si dispone di versioni precedenti e [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] più recenti delle cartelle di lavoro salvate nelle raccolte documenti della farm. Se gli analisti dell'organizzazione usano la versione [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel e salvano le cartelle di lavoro in un'installazione di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], la cartella di lavoro precedente non funziona. La relativa stringa di connessione farà riferimento a una versione precedente del provider, che non si troverà sul server a meno che non venga installata. L'installazione di entrambe le versioni consentirà l'accesso ai dati per le cartelle di lavoro di PowerPivot create con versioni precedenti e più recenti di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel. Il programma di installazione di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] non prevede l'installazione della versione [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del provider. È pertanto necessario installarla manualmente se si utilizzano cartelle di lavoro di una versione precedente.  
  
 **Il secondo scenario** si verifica quando si dispone di un server in una farm di SharePoint in cui viene eseguito [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]Excel Services, ma non. In questo caso, è necessario aggiornare manualmente il server applicazioni in cui viene eseguito Excel Services per poter utilizzare una versione più recente del provider. Ciò è necessario per la connessione a un'istanza di PowerPivot per SharePoint. Se Excel Services utilizza una versione meno recente del provider, la richiesta di connessione non riuscirà. Si noti che il provider deve essere installato tramite il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il pacchetto di installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] (spPowerPivot.msi) per assicurarsi che tutti i componenti necessari per il supporto di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] siano installati.  
  
  
##  <a name="bkmk_sql11"></a>Installare il provider di OLE DB SQL Server 2012 in un server Excel Services utilizzando SQL Server installazione  
 Utilizzare le istruzioni seguenti per aggiungere il provider OLE DB e altri componenti di connettività client ai server SharePoint in cui non è ancora installato, quali i server applicazioni in cui viene eseguito Excel Services, ma nei quali non è installato PowerPivot per SharePoint nello stesso hardware.  
  
 Utilizzare queste istruzioni per installare il provider di OLE DB Analysis Services corrente e per aggiungere **Microsoft. AnalysisServices. XMLA. dll** all'assembly globale.  
  
#### <a name="run-sql-server-setup-and-install-the-client-connectivity-tools"></a>Eseguire il programma di installazione di SQL Server e installare gli strumenti di connettività client  
  
1.  Nel server applicazioni che ospita Excel Services, eseguire il programma di installazione di SQL Server.  
  
2.  Nella pagina installazione scegliere **nuovo SQL Server installazione autonoma di o aggiunta di funzionalità a un'installazione esistente**.  
  
3.  Nella pagina tipo di installazione scegliere **Esegui una nuova installazione di SQL Server 2012**.  
  
4.  Nella pagina Impostazione ruolo scegliere **SQL Server installazione della funzionalità**.  
  
5.  Nella pagina **Selezione funzionalità** fare clic su **connettività strumenti client**. Questa opzione consente di installare **Microsoft. AnalysisServices. XMLA. dll**  
  
     Non selezionare altre funzionalità.  
  
6.  Fare clic su **Avanti** per terminare la procedura guidata, quindi fare clic su **Installa** per eseguire il programma di installazione.  
  
7.  Ripetere i passaggi precedenti se sono presenti altri server che eseguono Excel Services, senza un'installazione di PowerPivot per SharePoint sullo stesso server.  
  
#### <a name="verify-msolap5-is-a-trusted-provider"></a>Verificare che MSOLAP.5 sia un provider attendibile.  
  
1.  In Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**, quindi fare clic sull'applicazione di servizio Excel Services.  
  
2.  Fare clic su **Provider di dati attendibili**.  
  
3.  Verificare che MSOLAP.5 sia visualizzato nell'elenco. A seconda di come è stato configurato PowerPivot per SharePoint, MSOLAP.5 potrebbe già essere considerato attendibile. Se è stato utilizzato lo strumento di configurazione PowerPivot, ma questa azione è stata successivamente esclusa dall'elenco attività, MSOLAP.5 non sarà considerato attendibile da Excel Services e dovrà pertanto essere aggiunto manualmente.  
  
4.  Se MSOLAP non è elencato, fare clic su **aggiungi provider di dati attendibile**.  
  
5.  In ID provider, digitare `MSOLAP.5`.  
  
6.  Per Tipo di provider, assicurarsi che sia selezionato OLE DB.  
  
7.  In Descrizione provider digitare **Provider Microsoft OLE DB per OLAP Services 11.0**.  
  
#### <a name="verify-installation"></a>Verificare l'installazione  
  
1.  Spostarsi nella cartella Programmi\Microsoft Analysis Services\AS OLEDB\110.  
  
2.  Fare clic con il pulsante destro del mouse sul file msolap110.dll e scegliere **Proprietà**.  
  
3.  Fare clic su **Dettagli**.  
  
4.  Visualizzare le informazioni sulla versione del file. La versione deve includere 11,00. \<> BuildNumber.  
  
5.  Nella cartella Windows\assembly, verificare che venga elencato Microsoft.AnalysisServices.Xmla.dll, versione 11.0.0.0.  
  
  
##  <a name="bkmk_install2012_from_sppowerpivot_msi"></a>Usare il pacchetto di installazione di PowerPivot per SharePoint (spspPowerPivot. msi) per installare il provider di OLE DB SQL Server 2012  
 Installare il [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] Provider di OLE DB in e il server Excel Services utilizzando [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] il pacchetto di installazione di **(spspPowerPivot. msi)**.  
  
#### <a name="download-the-msolap5-provider-from-the-sssql11sp1-feature-pack"></a>Scaricare il provider MSOLAP.5 dal Feature Pack di [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] .  
  
1.  Passare a [Microsoft® SQL Server® 2012 SP1 Feature Pack](https://www.microsoft.com/download/details.aspx?id=35580)  
  
2.  Fare clic su **istruzioni di installazione**.  
  
3.  Vedere la sezione "Provider OLE DB Microsoft Analysis Services per Microsoft SQL Server 2012 SP1". Scaricare il file e avviare l'installazione.  
  
4.  Nella pagina **Selezione funzionalità** selezionare **provider OLE DB Analysis Services per SQL Server**. Deselezionare gli altri componenti e completare l'installazione. Per altre informazioni su spPowerPivot. msi, vedere [installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013).  
  
5.  Registrare MSOLAP.5 come provider attendibile con Excel Services di SharePoint. Per ulteriori informazioni, vedere [Aggiungere MSOLAP.5 come provider di dati attendibile in Excel Services](https://technet.microsoft.com/library/hh758436.aspx).  
  
  
##  <a name="bkmk_kj"></a>Installare il provider OLE DB 2008 SQL Server R2 per ospitare le cartelle di lavoro della versione precedente  
 Utilizzare le istruzioni seguenti per installare la versione [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del provider MSOLAP.4 e registrare il file Microsoft.AnalysisServices.ChannelTransport.dll. ChannelTransport è un sottocomponente del provider OLE DB di Analysis Services. Con la versione [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del provider è possibile leggere il Registro di sistema in caso di utilizzo di ChannelTransport per stabilire una connessione. La registrazione di questo file è un passaggio post-installazione obbligatorio solo per le connessioni gestite dal provider [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] in un server [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
#### <a name="step-1-download-and-install-the-client-library"></a>Passaggio 1: Scaricare e installare la libreria client  
  
1.  Nella [pagina SQL Server 2008 R2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=44272)trovare provider OLE DB Microsoft Analysis Services per Microsoft SQL Server 2008 R2.  
  
2.  Scaricare il pacchetto per x64 del programma di installazione `SQLServer2008_ASOLEDB10.msi`. Anche se nel nome file è incluso SQLServer2008, si tratta comunque del file corretto per la versione SQL Server 2008 R2 del provider.  
  
3.  Nel computer in cui è installato [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], eseguire il file con estensione msi per installare la libreria.  
  
4.  Se si dispone di altri server nella farm che eseguono solo Excel Services, senza [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] nello stesso server, ripetere i passaggi precedenti per installare la versione 2008 R2 del provider nel computer Excel Services.  
  
#### <a name="step-2-register-the-microsoftanalysisserviceschanneltransportdll-file"></a>Passaggio 2: Registrare il file Microsoft.AnalysisServices.ChannelTransport.dll  
  
1.  Utilizzare l'utilità regasm.exe per registrare il file. Se Regasm. exe non è stato eseguito in precedenza, aggiungere la relativa cartella padre\\, C:\Windows\Microsoft.NET\Framework64\v4.0.30319, alla variabile del percorso di sistema.  
  
2.  Aprire un prompt dei comandi con autorizzazioni di amministratore.  
  
3.  Andare alla cartella C:\Windows\assembly\GAC_MSIL\Microsoft.AnalysisServices.ChannelTransport\10.0.0.0__89845dcd8080cc91.  
  
4.  Immettere il comando seguente: `regasm microsoft.analysisservices.channeltransport.dll`  
  
5.  Ripetere i passaggi precedenti per qualsiasi computer nel quale è stata installata manualmente la versione 2008 R2 del provider.  
  
#### <a name="verify-installation"></a>Verificare l'installazione  
  
1.  A questo punto si dovrebbe essere in grado di applicare un filtro dati o di filtrare le cartelle di lavoro [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. In caso di errore, verificare che sia stata utilizzata la versione a 64 bit di regasm.exe per registrare il file.  
  
2.  Inoltre, è possibile controllare la versione del file.  
  
     Passare a `C:\Program files\Microsoft Analysis Services\AS OLEDB\10`. Fare clic con il pulsante destro del mouse su **msolap100. dll** e selezionare **Proprietà**. Fare clic su **Dettagli**.  
  
     Visualizzare le informazioni sulla versione del file. La versione deve includere 10,50. \<> BuildNumber.  
  
  
## <a name="see-also"></a>Vedere anche  
 [PowerPivot for SharePoint 2010 Installation](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
