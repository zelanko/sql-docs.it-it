---
title: Esegue l'analisi guidata di distribuzione di servizi | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d459bafe395a10af75f8c0a721f0a8a08f39b3c6
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509679"
---
# <a name="running-the-analysis-services-deployment-wizard"></a>Esecuzione della Distribuzione guidata Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuzione guidata può essere eseguito le seguenti:  
  
-   **In modo interattivo** quando esegue in modo interattivo, la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuzione guidata genera uno script di distribuzione basato su file di input, come modificata in modo interattivo dall'input dell'utente. Tramite la procedura guidata eventuali modifiche apportate dall'utente vengono applicate solo allo script di distribuzione. I file di input non vengono modificati. Per altre informazioni sui file di input, vedere [Informazioni sui file di input usati per creare uno script di distribuzione](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md).  
  
-   **Dal prompt dei comandi** quando viene eseguita al prompt dei comandi di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuzione guidata genera uno script di distribuzione basato alle opzioni utilizzabili per eseguire la procedura guidata. Tramite la procedura guidata potrebbe venire richiesto l'input dell'utente e potrebbero venire modificati i file di input in base a tale input, potrebbe venire eseguita una distribuzione automatica invisibile all'utente oppure potrebbe venire creato uno script di distribuzione da utilizzare successivamente.  
  
## <a name="running-the-analysis-services-deployment-wizard-interactively"></a>Esecuzione della Distribuzione guidata Analysis Services in modo interattivo  
 Quando viene eseguita in modo interattivo, la Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] legge i valori dei file di input e presenta le relative informazioni agli utenti. È possibile modificare questi valori, quali input come destinazione di distribuzione, le impostazioni di configurazione, le opzioni di distribuzione e password della stringa di connessione- o lasciarli inalterati. Se si modificano i valori di input, la procedura guidata Usa queste modifiche durante la generazione di script di distribuzione. Tramite la procedura guidata non vengono tuttavia apportate modifiche al file di input.  
  
> [!NOTE]  
>  Se si desidera utilizzare la Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per modificare i valori di input, eseguire la procedura guidata al prompt dei comandi e impostarla per l'esecuzione in modalità file di risposte.  
  
 Dopo aver esaminato i valori di input e rendere apportato le modifiche desiderate, la procedura guidata genera script di distribuzione. È possibile eseguire questo script di distribuzione immediatamente nel server di destinazione o salvarlo per utilizzarlo successivamente.  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-interactively"></a>Per eseguire la Distribuzione guidata Analysis Services in modo interattivo  
  
-   Fare clic su **avviare** > **di Microsoft SQL Server** > **distribuzione guidata**.  
  
     oppure  
  
-   Nel **progetti** cartella del [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del progetto, fare doppio clic su di \<nome progetto > file con estensione asdatabase.
    > [!NOTE]  
    >  Se non si trova il file con estensione asdatabase, provare a usare ricerca e specificare asdatabase. In alternativa, potrebbe essere necessario compilare il progetto in SSDT.  
  
## <a name="running-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>Esecuzione della Distribuzione guidata Analysis Services al prompt dei comandi  
 La Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] può essere inoltre eseguita al prompt dei comandi. In tal caso, è necessario specificare il percorso completo del file con estensione .asdatabase ed eseguire la procedura guidata in una delle modalità indicate di seguito.  
  
 **Modalità file di risposte**  
 In modalità file di risposte è possibile modificare in modo interattivo i file di input originariamente generati al durante la creazione del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. La procedura guidata Salva file di input modificati prima di generare lo script di distribuzione. I file di input modificati diventano il nuovo punto di partenza per la successiva esecuzione della procedura guidata.  
  
 Per eseguire la procedura guidata in modalità file di risposte, usare il **/a** passare.  
  
 **Modalità automatica**  
 In modalità non interattiva viene eseguita una distribuzione automatica invisibile all'utente basata sulle informazioni incluse nei file di input.  
  
 Per eseguire la procedura guidata in modalità non interattiva, usare il **/s** passare. Quando si esegue la procedura guidata in modalità non interattiva, i messaggi vengono inviati alla console o a un file di log, se presente.  
  
 **Modalità output**  
 In modalità output, la procedura guidata genera uno script di distribuzione per un'esecuzione successiva in base ai file di input.  
  
 Per eseguire la procedura guidata in modalità output, usare il **/o** passare e fornire un nome di file di output.  
  
 Per altre informazioni sulle opzioni della riga di comando, vedere [Distribuire soluzioni di modelli con l'utilità di distribuzione](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md).  
  
 Nella procedura seguente viene illustrato come eseguire la Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al prompt dei comandi.  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>Per eseguire la Distribuzione guidata Analysis Services al prompt dei comandi  
  
1.  Aprire un prompt dei comandi e passare al \Microsoft SQL Server\140\Tools\Binn\ManagementStudio C:\Program Files (x86)  
  
2.  Digitare **Microsoft.AnalysisServices.Deployment.exe** seguito dalle opzioni corrispondenti alla modalità in cui si desidera eseguire la procedura guidata.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sullo script di distribuzione di Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)   
 [Deploy Model Solutions Using the Deployment Wizard](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
