---
title: Distribuire soluzioni PowerPivot in SharePoint | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cc0286a3799aa56090fc6861b0a79b302b47aa26
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544274"
---
# <a name="deploy-power-pivot-solutions-to-sharepoint"></a>Distribuire soluzioni PowerPivot in SharePoint
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Usare le istruzioni seguenti per distribuire manualmente due pacchetti di soluzioni che consentono di aggiungere funzionalità di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a un ambiente SharePoint Server 2010. La distribuzione delle soluzioni è un passaggio obbligatorio per la configurazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint in un server SharePoint 2010. Per visualizzare l'elenco completo di procedure necessarie, vedere [Amministrazione e configurazione del server PowerPivot in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
 In alternativa, per distribuire le soluzioni è possibile usare lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . L'utilizzo dello strumento di configurazione è più facile e più efficiente per installazione di un unico server, ma è possibile utilizzare Amministrazione centrale e PowerShell se si preferisce utilizzare uno strumento familiare o se si configurano più funzionalità contemporaneamente. Per altre informazioni sull'uso dello strumento di configurazione, vedere [Strumenti di configurazione di PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
 Prima della distribuzione delle soluzioni è necessario installare [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint tramite il supporto di installazione di SQL Server 2012. I pacchetti di soluzioni che si desidera distribuire verranno installati dal programma di installazione di SQL Server.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Prerequisito: Verificare che l'applicazione Web utilizzi l'autenticazione in modalità classica](#bkmk_classic)  
  
 [Passaggio 1: Distribuire la soluzione Farm](#bkmk_farm)  
  
 [Passaggio 2: Distribuire la soluzione applicazione Web PowerPivot in Amministrazione centrale](#deployCA)  
  
 [Passaggio 3: Distribuire la soluzione applicazione Web PowerPivot ad altre applicazioni Web](#deployUI)  
  
 [Ridistribuire o ritirare la soluzione](#retract)  
  
 [Informazioni sulle soluzioni PowerPivot](#intro)  
  
##  <a name="bkmk_classic"></a> Prerequisito: Verificare che l'applicazione Web utilizzi l'autenticazione in modalità classica  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint è supportato solo per le applicazioni Web che usano l'autenticazione in modalità classica di Windows. Per controllare se l'applicazione usa la modalità di distribuzione classica, eseguire il cmdlet di PowerShell seguente dal **Shell di gestione SharePoint 2010**, sostituendo **http://\<nome sito di livello superiore >** con il nome del sito di SharePoint:  
  
```  
Get-spwebapplication http://<top-level site name> | format-list UseClaimsAuthentication  
```  
  
 Il valore restituito dovrebbe essere **false**. Se **true**, non è possibile accedere ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] con questa applicazione Web.  
  
##  <a name="bkmk_farm"></a> Passaggio 1: Distribuire la soluzione Farm  
 Questa sezione illustra come distribuire le soluzioni usando PowerShell, ma è anche possibile usare lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per completare questa attività. Per altre informazioni, vedere [Configurare o ripristinare PowerPivot per SharePoint 2010 (strumento di configurazione PowerPivot)](http://msdn.microsoft.com/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
 È necessario eseguire questa attività una sola volta dopo l'installazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint.  
  
1.  Su un server che dispone di un'installazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint, aprire una shell di gestione di SharePoint 2010 tramite l'opzione **Esegui come amministratore** .  
  
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
 Dopo la distribuzione della soluzione farm, è necessario distribuire la soluzione applicazione Web in Amministrazione centrale. Tramite questo passaggio viene aggiunto il dashboard di gestione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in Amministrazione centrale.  
  
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
 Nell'attività precedente si è distribuito Powerpivotwebapp.wsp in Amministrazione centrale. In questa sezione si provvederà alla distribuzione di powerpivotwebapp.wsp in un'applicazione Web esistente che supporta l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Se in seguito si aggiungono altre applicazioni Web, assicurarsi di ripetere questo passaggio anche per tali applicazioni.  
  
1.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci soluzioni farm**.  
  
2.  Fare clic su **powerpivotwebapp.wsp**.  
  
3.  Fare clic su **Distribuisci soluzione**.  
  
4.  In **Destinazione distribuzione**selezionare l'applicazione Web di SharePoint per cui si desidera aggiungere supporto alle funzionalità di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
5.  Fare clic su **OK**.  
  
6.  Ripetere l'operazione per le altre applicazioni Web SharePoint che supporteranno l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
##  <a name="retract"></a> Ridistribuire o ritirare la soluzione  
 Sebbene Amministrazione centrale SharePoint consenta il ritiro della soluzione, non è necessario ritirare il file powerpivotwebapp.wsp a meno che si stia sistematicamente eseguendo la risoluzione dei problemi relativi a un'installazione o alla distribuzione di una patch.  
  
1.  In Impostazioni sistema di Amministrazione centrale SharePoint 2010 fare clic su **Gestisci soluzioni farm**.  
  
2.  Fare clic su **Powerpivotwebapp.wsp**.  
  
3.  Fare clic su **Ritira soluzione**.  
  
 Se si verificano problemi relativi alla distribuzione server che risalgono alla soluzione farm, è possibile ridistribuirla eseguendo l'opzione **Ripristina** nello strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Le operazioni di ripristino tramite lo strumento sono preferibili perché richiedono meno passaggi da parte dell'utente. Per altre informazioni, vedere [Configurare o ripristinare PowerPivot per SharePoint 2010 (strumento di configurazione PowerPivot)](http://msdn.microsoft.com/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
 Se si desidera ridistribuire ancora tutte le soluzioni, assicurarsi di effettuare le operazioni in questo ordine:  
  
1.  Ritirare la soluzione dell'applicazione Web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] da tutte le applicazioni Web SharePoint in cui viene usata.  
  
2.  Ritirare la soluzione farm [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]  
  
3.  Ridistribuire la soluzione farm [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]  
  
4.  Ridistribuire la soluzione dell'applicazione Web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in tutte le applicazioni Web SharePoint.  
  
##  <a name="intro"></a> Informazioni sulle soluzioni PowerPivot  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint usa due pacchetti di soluzioni per distribuire le relative pagine dell'applicazione e file di programma nella farm e in singole applicazioni Web.  
  
-   La soluzione farm è globale. Viene distribuita una volta e quindi diventa automaticamente disponibile in qualsiasi nuovo server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint che verrà aggiunto alla farm.  
  
-   La soluzione dell'applicazione Web è specifica dell'applicazione e deve essere distribuita a ogni applicazione Web nella farm, inclusa l'applicazione Web Amministrazione centrale.  
  
 Ogni soluzione viene distribuita in modo diverso.  La soluzione della farm viene distribuita una volta, dopo l'installazione della prima istanza di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint. Per distribuire la soluzione farm, usare lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o i cmdlet PowerShell.  
  
 La soluzione applicazione Web viene inizialmente distribuita ad Amministrazione centrale, seguita dalle distribuzioni successive della soluzione a qualsiasi applicazione Web aggiuntiva che supporterà le richieste di dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Per distribuire la soluzione applicazione Web in Amministrazione centrale, è necessario usare lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o il cmdlet PowerShell. Per tutte le altre applicazioni Web, è possibile distribuire la soluzione applicazione Web manualmente utilizzando Amministrazione centrale o PowerShell.  
  
|Soluzione|Descrizione|  
|--------------|-----------------|  
|Powerpivotfarm.wsp|Consente di aggiungere il file Microsoft.AnalysisServices.SharePoint.Integration.dll all'assembly globale.<br /><br /> Consente di aggiungere il file Microsoft.AnalysisServices.ChannelTransport.dll all'assembly globale.<br /><br /> Consente di installare funzionalità e file di risorse nonché di registrare i tipi di contenuto.<br /><br /> Aggiunge modelli di raccolta per Raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e le raccolte di feed di dati.<br /><br /> Aggiunge pagine dell'applicazione per la configurazione dell'applicazione del servizio, il dashboard di gestione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , l'aggiornamento dati e la raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|powerpivotwebapp.wsp|Aggiunge i file di risorse Microsoft.AnalysisServices.SharePoint.Integration.dll alla cartella delle estensioni per il server Web nel server Web front-end.<br /><br /> Aggiunge il servizio Web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] al server Web front-end.<br /><br /> Aggiunge la generazione di immagini di anteprima per Raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornare Power Pivot per SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Amministrazione e configurazione del server PowerPivot in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Configurazione di Power Pivot con Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
  
