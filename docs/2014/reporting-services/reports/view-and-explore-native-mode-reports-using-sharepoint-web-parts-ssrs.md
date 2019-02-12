---
title: Visualizzare ed esplorare i report in modalità nativa usando le web part di SharePoint (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: dee8ee42-156b-43b6-b202-02dfb9404284
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 17706542014f3835cb0a100d7dbf3e579b47aa65
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56010659"
---
# <a name="view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs"></a>View and Explore Native Mode Reports Using SharePoint Web Parts (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include diverse web part che funzionano con versioni specifiche di un server di report e in determinate modalità di distribuzione.  
  
-   **Modalità nativa:** se si desidera accedere al contenuto di un server di report in un sito di SharePoint da un server di report eseguito in modalità nativa, utilizzare le web part Esplora report e Visualizzatore report di SharePoint 2.0 incluse in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. In questo argomento sono disponibili le istruzioni per l'installazione e l'utilizzo delle web part della versione 2.0.  
  
-   **Modalità SharePoint:** se si desidera accedere a un server di report eseguito in modalità SharePoint, utilizzare le web part installate dal componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per prodotti SharePoint. Per altre informazioni sui componenti aggiuntivi, vedere [Posizione in cui trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
-   > [!NOTE]  
    >  La web part Visualizzatore report per la modalità nativa (SPViewer.dwp) è diversa da quella (ReportViewer.dwp) installata dal componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per prodotti SharePoint. Nelle web part sono inclusi schemi e implementazioni diversi, tuttavia possono essere installate entrambe nella stessa farm SharePoint. È possibile distinguere le web part visivamente grazie alle caratteristiche seguenti: nella web part Visualizzatore report, installata tramite il componente aggiuntivo, è disponibile un menu **Azioni** sulla barra degli strumenti.  
  
 Per altre informazioni sulle modalità del server di report, vedere [Server di report di Reporting Services](../reporting-services-report-server.md).  
  
 Contenuto dell'argomento:  
  
-   [Informazioni su Report Explorer e Visualizzatore report](#bkmk_aboutwebparts)  
  
-   [Requisiti per l'utilizzo delle web part](#bkmk_requirements)  
  
-   [Installazione di web part](#bkmk_installingwebparts)  
  
-   [Aggiungere e configurare web part](#bkmk_configurewebparts)  
  
##  <a name="bkmk_aboutwebparts"></a> Informazioni su Report Explorer e Visualizzatore report  
 Report Explorer e Visualizzatore report sono web part di SharePoint 2.0 introdotte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Service Pack 2 (SP2) e ancora disponibili nelle versioni correnti.  
  
 Tramite le web part viene offerto un modo per visualizzare i report ed esplorare la gerarchia di cartelle del server di report da un sito di SharePoint.  
  
 Si noti che non sono supportate funzionalità di personalizzazione delle web part. Le web part sono concepite per essere utilizzate come sono e non devono essere estese o modificate.  
  
-   Con**Esplora report** (SPExplorer.dwp) è possibile connettersi a Gestione report nel computer del server di report. È possibile esplorare i report disponibili in un server di report e sottoscrivere singoli report. Se Generatore report è abilitato e si dispone di autorizzazioni sufficienti, è possibile avviare Generatore report dalla web part Report Explorer.  
  
     Report Explorer consente di visualizzare i contenuti di una cartella utilizzando una pagina di Gestione report. L'accesso a singoli elementi e cartelle nella gerarchia di cartelle del server di report viene controllato mediante l'assegnazione di ruoli nel server di report. Quando si seleziona un report, quest'ultimo viene aperto in una nuova finestra del browser. Il report viene visualizzato nel Visualizzatore HTML del server di report, il quale include la barra degli strumenti per report, non nella web part Visualizzatore report. Se si desidera personalizzare le impostazioni della barra degli strumenti, accertarsi di specificare i parametri di accesso all'URL nel server di report. Per istruzioni, vedere [Riferimento ai parametri di accesso con URL](../url-access-parameter-reference.md).  
  
-   Con**Visualizzatore report** (SPViewer.dwp) è possibile visualizzare un report e viene fornita una barra degli strumenti utilizzabile per navigare tra le pagine, eseguire ricerche nel contenuto o esportare il report. È possibile aggiungere la web part Visualizzatore report a una pagina web part in modo che in quest'ultima venga sempre visualizzato un determinato report oppure **è possibile connettersi a Esplora report** per visualizzare i report aperti tramite questa web part.  
  
##  <a name="bkmk_requirements"></a> Requisiti per l'utilizzo delle web part  
 I requisiti per l'utilizzo delle web part Visualizzatore report e Report Explorer includono quanto segue:  
  
-   Le versioni supportate di prodotti e tecnologie SharePoint sono:  
  
    -   [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 e [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007.  
  
    -   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] e [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
-   La versione del server di report in modalità nativa deve essere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o successiva.  
  
-   Il server di report deve essere eseguito in modalità nativa. **Non** è possibile utilizzare le web part Esplora report e Visualizzatore report per visualizzare o connettersi a report in un server di report eseguito in modalità SharePoint.  
  
-   Gestione report deve essere installato.  
  
 Le web part Report Explorer e Visualizzatore report sono distribuite tramite un file CAB (con estensione cab) incluso in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Nelle sezioni seguenti di questo argomento sono disponibili istruzioni per installare, configurare e utilizzare le web part.  
  
##  <a name="bkmk_installingwebparts"></a> Installazione di web part  
 Le web part vengono recapitate a un server SharePoint come file CAB. Per installare le web part, eseguire lo strumento Stsadm.exe di SharePoint incluso nel file con estensione cab dalla riga di comando. Per ulteriori informazioni sullo strumento e la distribuzione delle web part, vedere la documentazione di SharePoint.  
  
#### <a name="install-web-parts-using-powershell"></a>Installare web part tramite PowerShell  
  
1.  Copiare il file **RSWebParts.cab** in una cartella nel server SharePoint. È possibile copiare il file in qualsiasi cartella nel server di SharePoint e quindi eliminarlo dopo aver installato le web part. Per impostazione predefinita, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installa il file RSWebParts.cab nella cartella seguente:  
  
    ```  
    C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint  
    ```  
  
2.  Nel computer in cui è disponibile l'installazione del prodotto SharePoint aprire **Shell di gestione SharePoint 2010** con **privilegi amministrativi**.  
  
3.  Eseguire il comando PowerShell seguente:  
  
    ```  
    Install-SPWebPartPack -LiteralPath "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -GlobalInstall  
    ```  
  
4.  Si dovrebbe visualizzare un messaggio simile al seguente, in cui viene indicata la distribuzione della web part.  
  
    > Name               SolutionId                                             Deployed  
  
    > ----                    ----------                                              -------\-  
  
    > rswebparts.cab    00000000-0000-0000-0000-000000000000     True  
  
     Per altre informazioni sull'uso di PowerShell, vedere [Install-SPWebPartPack (https://technet.microsoft.com/library/ff607840.aspx)](https://technet.microsoft.com/library/ff607840.aspx).  
  
#### <a name="install-web-parts-using-stsadmexe"></a>Installare web part tramite STSADM.exe  
  
1.  Copiare il file **RSWebParts.cab** nello stesso percorso del server SharePoint come descritto nella sezione relativa a PowerShell presente in questo documento.  
  
2.  Nel computer in cui è disponibile l'installazione del prodotto SharePoint, aprire una finestra del prompt dei comandi con privilegi amministrativi e passare alla cartella contenente lo strumento **Stsadm.exe** . Il percorso predefinito per [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] è il seguente:  
  
    > C:\Programmi\Common Files\Microsoft Shared\Web Server Extensions\14\BIN.  
  
3.  Eseguire Stsadm.exe incluso nel file con estensione cab con la sintassi seguente:  
  
    ```  
    STSADM.EXE -o addwppack -filename "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -globalinstall  
    ```  
  
4.  Si dovrebbe visualizzare un messaggio relativo al corretto completamento dell'operazione.  
  
     Se si specifica `-globalinstall` , le web part verranno aggiunte alla Global Assembly Cache (GAC). Questo passaggio è necessario se si desidera connettersi alle web part.  
  
##  <a name="bkmk_configurewebparts"></a> Aggiungere e configurare web part  
 Dopo aver installato le web part, è possibile aggiungerle a una o più pagine web in un sito di SharePoint. È necessario disporre dell'autorizzazione per creare siti Web e aggiungere contenuto.  
  
 Con la procedura riportata di seguito sarà possibile aggiungere entrambe le web part a una pagina e, successivamente, collegare Esplora report e Visualizzatore report in modo che quando si fa clic su un report in Esplora report, questo sarà visualizzato in Visualizzatore report.  
  
#### <a name="add-report-viewer"></a>Aggiungere Visualizzatore report  
  
1.  In Azioni sito fare clic su **Modifica pagina**.  
  
2.  In una zona della pagina fare clic su **Aggiungi web part**.  
  
3.  Nella finestra di dialogo **Aggiungi web part** scorrere fino alla categoria **Varie** .  
  
4.  Selezionare **Visualizzatore report**.  
  
    > [!WARNING]  
    >  Non selezionare **Visualizzatore report di SQL Server Reporting Services** . Questa web part viene registrata quando si installa il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per prodotti SharePoint e viene usata per l'esecuzione di un server di report in modalità SharePoint. Non è possibile utilizzarla per visualizzare i report in un server di report eseguito in modalità nativa.  
  
5.  Scegliere **Aggiungi**.  
  
6.  In modalità di modifica della pagina fare clic su **Modifica web part** nella web part Visualizzatore report.  
  
7.  In **Report Manager URL**digitare l'URL di un'istanza di Gestione report associata al server di report in modalità nativa a cui si desidera accedere. Per impostazione predefinita, la sintassi dell'URL di Gestione report è la seguente: **http://\<nomeserver>/reports**.  
  
8.  In **Percorso report**specificare una barra seguita dal percorso della cartella e dal nome del report. **Non** includere il nome del server o la directory virtuale di Gestione report. Ad esempio, per aprire il report "Company Sales" nella cartella Adventure Works, specificare **/Adventure Works/Company Sales**. Di seguito è riportato un altro esempio in cui il report "Products" si trova nella cartella radice del server di report **/Products**.  
  
9. Fare clic su **OK**.  
  
#### <a name="add-report-explorer-and-connect-to-report-viewer"></a>Aggiungere Esplora report ed effettuare il collegamento a Visualizzatore report  
  
1.  In un'altra area della pagina fare clic su **Aggiungi web part** e nella cartella Varie selezionare **Esplora report** , quindi **Aggiungi**.  
  
2.  Nel menu di scelta rapida della web part Esplora report fare clic su **Modifica web part**.  
  
3.  In **Report Manager URL**digitare l'URL di un'istanza di Gestione report associata al server di report in modalità nativa a cui si desidera accedere.  
  
4.  Facoltativamente, impostare il **Percorso iniziale**. Il percorso iniziale rappresenta la cartella nella gerarchia di cartelle del server di report. È possibile specificare un percorso iniziale se si desidera che la pagina predefinita sia una cartella che si trova a un livello inferiore nella gerarchia. Il percorso deve iniziare con una barra. È necessario specificare un percorso completo che inizi con il nodo radice della gerarchia di cartelle del server di report, ma non includa il nome del server o la directory virtuale di Gestione report. Per aprire ad esempio una cartella denominata Adventure Works che si trova al livello immediatamente inferiore rispetto al nodo radice, specificare **/Adventure Works** come percorso iniziale.  
  
5.  Fare clic su **OK**.  
  
6.  In Esplora report verrà visualizzato un elenco degli elementi del report nel relativo server. Per impostazione predefinita, se si fa clic sul nome di un report, quest'ultimo verrà aperto in una nuova finestra. Completare i passaggi riportati di seguito se si desidera collegare Esplora report a Visualizzatore report in modo che quando si fa clic sul nome di un report in Esplora report, questo venga visualizzato in Visualizzatore report.  
  
    1.  Nel menu di scelta rapida di Esplora report fare clic su **Connessioni**.  
  
    2.  Fare clic su **Visualizza report in**.  
  
    3.  Fare clic su **Visualizzatore report**.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Server di report di Reporting Services &#40;modalità SharePoint&#41;](../reporting-services-report-server-sharepoint-mode.md)   
 [Reporting Services Report Server &#40;Native Mode&#41;](../report-server/reporting-services-report-server-native-mode.md)  
  
  
