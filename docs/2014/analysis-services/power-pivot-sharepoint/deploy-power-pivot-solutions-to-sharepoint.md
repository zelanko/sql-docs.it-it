---
title: Distribuire soluzioni PowerPivot in SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f202a2b7-34e0-43aa-90d5-c9a085a37c32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b568790f9a61c01054d4a7225e4a2dbf9a39887
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071511"
---
# <a name="deploy-powerpivot-solutions-to-sharepoint"></a>Distribuire soluzioni PowerPivot in SharePoint
  Utilizzare le seguenti istruzioni per distribuire manualmente due pacchetti di soluzioni che consentono di aggiungere funzionalità di PowerPivot a un ambiente SharePoint Server 2010. La distribuzione delle soluzioni è un passaggio obbligatorio per la configurazione di PowerPivot per SharePoint in un server SharePoint 2010. Per visualizzare l'elenco completo dei passaggi necessari, vedere [amministrazione Server PowerPivot e la configurazione in Amministrazione centrale](power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
 In alternativa, per distribuire le soluzioni è possibile utilizzare lo strumento di configurazione PowerPivot. L'utilizzo dello strumento di configurazione è più facile e più efficiente per installazione di un unico server, ma è possibile utilizzare Amministrazione centrale e PowerShell se si preferisce utilizzare uno strumento familiare o se si configurano più funzionalità contemporaneamente. Per altre informazioni sull'uso dello strumento di configurazione, vedere [strumenti di configurazione PowerPivot](power-pivot-configuration-tools.md).  
  
 Prima della distribuzione delle soluzioni è necessario installare PowerPivot per SharePoint tramite il supporto di installazione di SQL Server 2012. I pacchetti di soluzioni che si desidera distribuire verranno installati dal programma di installazione di SQL Server.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Prerequisito: Verificare che l'applicazione Web utilizzi l'autenticazione in modalità classica](#bkmk_classic)  
  
 [Passaggio 1: Distribuire la soluzione Farm](#bkmk_farm)  
  
 [Passaggio 2: Distribuire la soluzione applicazione Web PowerPivot in Amministrazione centrale](#deployCA)  
  
 [Passaggio 3: Distribuire la soluzione applicazione Web PowerPivot ad altre applicazioni Web](#deployUI)  
  
 [Ridistribuire o ritirare la soluzione](#retract)  
  
 [Informazioni sulle soluzioni PowerPivot](#intro)  
  
##  <a name="bkmk_classic"></a> Prerequisito: Verificare che l'applicazione Web utilizzi l'autenticazione in modalità classica  
 PowerPivot per SharePoint è supportato solo per le applicazioni Web che utilizzano l'autenticazione in modalità classica di Windows. Per controllare se l'applicazione usa la modalità di distribuzione classica, eseguire il cmdlet di PowerShell seguente dal **Shell di gestione SharePoint 2010**, sostituendo `http://<top-level site name>` con il nome del sito di SharePoint:  
  
```  
Get-spwebapplication http://<top-level site name> | format-list UseClaimsAuthentication  
```  
  
 Il valore restituito dovrebbe essere **false**. Se si tratta **true**, è possibile accedere ai dati di PowerPivot con questa applicazione web.  
  
##  <a name="bkmk_farm"></a> Passaggio 1: Distribuire la soluzione Farm  
 In questa sezione viene illustrato come distribuire le soluzioni utilizzando PowerShell, ma è anche possibile utilizzare lo strumento di configurazione PowerPivot per completare questa attività. Per altre informazioni, vedere [Configura o Ripristina PowerPivot per SharePoint 2010 &#40;strumento di configurazione PowerPivot&#41;](../configure-repair-powerpivot-sharepoint-2010.md).  
  
 È necessario eseguire questa attività una sola volta dopo l'installazione di PowerPivot per SharePoint.  
  
1.  In un server che dispone di un'installazione di PowerPivot per SharePoint, aprire una Shell di gestione SharePoint 2010 tramite il **Esegui come amministratore** opzione.  
  
2.  Eseguire il seguente cmdlet per aggiungere la soluzione farm.  
  
    ```  
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     Il cmdlet restituisce il nome e l'ID della soluzione e Deployed=False. Nel passaggio successivo la soluzione verrà distribuita.  
  
3.  Eseguire il successivo cmdlet per distribuire la soluzione farm:  
  
    ```  
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
##  <a name="deployCA"></a> Passaggio 2: Distribuire la soluzione applicazione Web PowerPivot in Amministrazione centrale  
 Dopo la distribuzione della soluzione farm, è necessario distribuire la soluzione applicazione Web in Amministrazione centrale. Tramite questo passaggio viene aggiunto il dashboard di gestione PowerPivot in Amministrazione centrale.  
  
1.  Aprire una shell di gestione di SharePoint 2010 utilizzando l'opzione **Esegui come amministratore** .  
  
2.  Eseguire il seguente cmdlet per creare un riferimento ad Amministrazione centrale:  
  
    ```  
    $centralAdmin = $(Get-SPWebApplication -IncludeCentralAdministration | Where { $_.IsAdministrationWebApplication -eq $TRUE})  
    ```  
  
3.  Eseguire il seguente cmdlet per aggiungere la soluzione farm.  
  
    ```  
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotWebApp.wsp"  
    ```  
  
     Il cmdlet restituisce il nome e l'ID della soluzione e Deployed=False. Nel passaggio successivo la soluzione verrà distribuita.  
  
4.  Eseguire il successivo cmdlet per installare la soluzione applicazione Web in Amministrazione centrale.  
  
    ```  
    Install-SPSolution -Identity PowerPivotWebApp.wsp -GACDeployment -Force -WebApplication $centralAdmin  
    ```  
  
 Dopo la distribuzione della soluzione applicazione Web in Amministrazione centrale, sarà possibile utilizzare questo strumento per completare tutti i passaggi di configurazione rimanenti.  
  
##  <a name="deployUI"></a> Passaggio 3: Distribuire la soluzione applicazione Web PowerPivot ad altre applicazioni Web  
 Nell'attività precedente si è distribuito Powerpivotwebapp.wsp in Amministrazione centrale. In questa sezione si provvederà alla distribuzione di powerpivotwebapp.wsp in un'applicazione Web esistente che supporta l'accesso ai dati PowerPivot. Se in seguito si aggiungono altre applicazioni Web, assicurarsi di ripetere questo passaggio anche per tali applicazioni.  
  
1.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci soluzioni farm**.  
  
2.  Fare clic su **powerpivotwebapp.wsp**.  
  
3.  Fare clic su **Distribuisci soluzione**.  
  
4.  Nelle **destinazione distribuzione?**, selezionare l'applicazione web di SharePoint per il quale si desidera aggiungere il supporto di funzionalità di PowerPivot.  
  
5.  Fare clic su **OK**.  
  
6.  Ripetere l'operazione per le altre applicazioni Web SharePoint che supporteranno l'accesso ai dati PowerPivot.  
  
##  <a name="retract"></a> Ridistribuire o ritirare la soluzione  
 Sebbene Amministrazione centrale SharePoint consenta il ritiro della soluzione, non è necessario ritirare il file powerpivotwebapp.wsp a meno che si stia sistematicamente eseguendo la risoluzione dei problemi relativi a un'installazione o alla distribuzione di una patch.  
  
1.  In Impostazioni sistema di Amministrazione centrale SharePoint 2010 fare clic su **Gestisci soluzioni farm**.  
  
2.  Fare clic su **Powerpivotwebapp.wsp**.  
  
3.  Fare clic su **Ritira soluzione**.  
  
 Se si verificano problemi di distribuzione server che risalgono alla soluzione farm, è possibile ridistribuirla eseguendo il **Repair** opzione nello strumento di configurazione PowerPivot. Le operazioni di ripristino tramite lo strumento sono preferibili perché richiedono meno passaggi da parte dell'utente. Per altre informazioni, vedere [Configura o Ripristina PowerPivot per SharePoint 2010 &#40;strumento di configurazione PowerPivot&#41;](../configure-repair-powerpivot-sharepoint-2010.md).  
  
 Se si desidera ridistribuire ancora tutte le soluzioni, assicurarsi di effettuare le operazioni in questo ordine:  
  
1.  Ritirare la soluzione dell'applicazione Web PowerPivot da tutte le applicazioni Web SharePoint in cui viene utilizzata.  
  
2.  Ritirare la soluzione farm PowerPivot.  
  
3.  Ridistribuire la soluzione farm PowerPivot.  
  
4.  Ridistribuire la soluzione dell'applicazione Web PowerPivot in tutte le applicazioni Web SharePoint.  
  
##  <a name="intro"></a> Informazioni sulle soluzioni PowerPivot  
 In PowerPivot per SharePoint vengono utilizzati due pacchetti di soluzioni per distribuire le relative pagine dell'applicazione e file di programma nella farm e in singole applicazioni Web.  
  
-   La soluzione farm è globale. Viene distribuita una volta e quindi diventa automaticamente disponibile in qualsiasi nuovo server PowerPivot per SharePoint che verrà aggiunto alla farm.  
  
-   La soluzione dell'applicazione Web è specifica dell'applicazione e deve essere distribuita a ogni applicazione Web nella farm, inclusa l'applicazione Web Amministrazione centrale.  
  
 Ogni soluzione viene distribuita in modo diverso.  La soluzione della farm viene distribuita una volta, dopo l'installazione della prima istanza di PowerPivot per SharePoint. Per distribuire la soluzione farm, utilizzare lo strumento di configurazione PowerPivot o i cmdlet PowerShell.  
  
 La soluzione applicazione Web viene inizialmente distribuita ad Amministrazione centrale, seguita dalle distribuzioni successive della soluzione a qualsiasi applicazione Web aggiuntiva che supporterà le richieste di dati PowerPivot. Per distribuire la soluzione applicazione Web in Amministrazione centrale, è necessario utilizzare lo strumento di configurazione PowerPivot o il cmdlet PowerShell. Per tutte le altre applicazioni Web, è possibile distribuire la soluzione applicazione Web manualmente utilizzando Amministrazione centrale o PowerShell.  
  
|Soluzione|Descrizione|  
|--------------|-----------------|  
|Powerpivotfarm.wsp|Consente di aggiungere il file Microsoft.AnalysisServices.SharePoint.Integration.dll all'assembly globale.<br /><br /> Consente di aggiungere il file Microsoft.AnalysisServices.ChannelTransport.dll all'assembly globale.<br /><br /> Consente di installare funzionalità e file di risorse nonché di registrare i tipi di contenuto.<br /><br /> Aggiunge modelli di raccolta per Raccolta PowerPivot e le raccolte di feed di dati.<br /><br /> Aggiunge pagine dell'applicazione per la configurazione dell'applicazione di servizio, il dashboard di gestione di PowerPivot, l'aggiornamento dati e la raccolta PowerPivot.|  
|powerpivotwebapp.wsp|Aggiunge i file di risorse Microsoft.AnalysisServices.SharePoint.Integration.dll alla cartella delle estensioni per il server Web nel server Web front-end.<br /><br /> Aggiunge il servizio Web PowerPivot al server Web-front end.<br /><br /> Aggiunge la generazione di immagini di anteprima per Raccolta PowerPivot.|  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornare PowerPivot per SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Amministrazione Server PowerPivot e la configurazione in Amministrazione centrale](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Configurazione di PowerPivot tramite Windows PowerShell](power-pivot-configuration-using-windows-powershell.md)  
  
  
