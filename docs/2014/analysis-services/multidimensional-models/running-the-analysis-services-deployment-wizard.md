---
title: Esecuzione della distribuzione guidata Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, running
ms.assetid: 3a38d489-4625-4878-bd18-c6f903be33df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d8fd34a7e614c1c1bb247f84846e090d22ea053e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66073042"
---
# <a name="running-the-analysis-services-deployment-wizard"></a>Esecuzione della Distribuzione guidata Analysis Services
  Quando si utilizza la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuzione guidata per distribuire un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto, è possibile eseguire la procedura guidata nei modi seguenti:  
  
-   **In modo interattivo** Quando viene eseguita in modo interattivo, la Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente di generare uno script di distribuzione XML basato sui file in input, in base alle modifiche interattive apportate tramite l'input dell'utente. Tramite la procedura guidata eventuali modifiche apportate dall'utente vengono applicate solo allo script di distribuzione. I file di input non vengono modificati. Per altre informazioni sui file di input, vedere [Informazioni sui file di input usati per creare uno script di distribuzione](deployment-script-files-input-used-to-create-deployment-script.md).  
  
-   **Dal prompt dei comandi** Quando viene eseguito al prompt dei comandi, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] la distribuzione guidata genera uno script di distribuzione di XML for Analysis (XMLA) basato sulle opzioni utilizzate per eseguire la procedura guidata. Tramite la procedura guidata potrebbe venire richiesto l'input dell'utente e potrebbero venire modificati i file di input in base a tale input, potrebbe venire eseguita una distribuzione automatica invisibile all'utente oppure potrebbe venire creato uno script di distribuzione da utilizzare successivamente.  
  
## <a name="running-the-analysis-services-deployment-wizard-interactively"></a>Esecuzione della Distribuzione guidata Analysis Services in modo interattivo  
 Quando viene eseguita in modo interattivo, la Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] legge i valori dei file di input e presenta le relative informazioni agli utenti. È possibile modificare questi valori di input, ad esempio destinazione di distribuzione, impostazioni di configurazione, opzioni di distribuzione e password della stringa di connessione, oppure lasciarli invariati. Se si modificano i valori di input, le modifiche vengono utilizzate dalla procedura guidata per la creazione dello script di distribuzione XMLA. Tramite la procedura guidata non vengono tuttavia apportate modifiche al file di input.  
  
> [!NOTE]  
>  Se si desidera utilizzare la Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per modificare i valori di input, eseguire la procedura guidata al prompt dei comandi e impostarla per l'esecuzione in modalità file di risposte.  
  
 Dopo avere verificato i valori di input e avere apportato le modifiche desiderate, tramite la procedura guidata verrà generato uno script di distribuzione XMLA. È possibile eseguire questo script di distribuzione immediatamente nel server di destinazione o salvarlo per utilizzarlo successivamente.  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-interactively"></a>Per eseguire la Distribuzione guidata Analysis Services in modo interattivo  
  
-   Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server**, **Analysis Services**e quindi **Distribuzione guidata**.  
  
     -oppure-  
  
-   Nella cartella **progetti** del [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto fare doppio clic sul * \<nome del progetto>* file con estensione asdatabase.  
  
    > [!NOTE]  
    >  Se non è possibile trovare il * \<nome del progetto>* file asdatabase, provare a usare la ricerca e specificare *. asdatabase.  
  
## <a name="running-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>Esecuzione della Distribuzione guidata Analysis Services al prompt dei comandi  
 La Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] può essere inoltre eseguita al prompt dei comandi. In tal caso, è necessario specificare il percorso completo del file con estensione .asdatabase ed eseguire la procedura guidata in una delle modalità indicate di seguito.  
  
 **Modalità file di risposte**  
 In modalità file di risposte è possibile modificare in modo interattivo i file di input originariamente generati al durante la creazione del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. I file di input modificati vengono salvati tramite la procedura guidata prima di creare lo script di distribuzione XMLA. I file di input modificati diventano il nuovo punto di partenza per la successiva esecuzione della procedura guidata.  
  
 Per eseguire la procedura guidata in modalità file di risposte, usare l'opzione **/a** .  
  
 **Modalità automatica**  
 In modalità non interattiva viene eseguita una distribuzione automatica invisibile all'utente basata sulle informazioni incluse nei file di input.  
  
 Per eseguire la procedura guidata in modalità invisibile all'utente, usare l'opzione **/s** . Quando si esegue la procedura guidata in modalità non interattiva, i messaggi vengono inviati alla console o a un file di log, se presente.  
  
 **Modalità output**  
 In modalità output viene generato uno script di distribuzione XMLA da eseguire successivamente, basato sui file di input.  
  
 Per eseguire la procedura guidata in modalità output, usare l'opzione **/o** e specificare un nome di file di output.  
  
 Per altre informazioni sulle opzioni della riga di comando, vedere [Distribuire soluzioni di modelli con l'utilità di distribuzione](deploy-model-solutions-with-the-deployment-utility.md).  
  
 Nella procedura seguente viene illustrato come eseguire la Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al prompt dei comandi.  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>Per eseguire la Distribuzione guidata Analysis Services al prompt dei comandi  
  
1.  Aprire il prompt dei comandi e passare alla cartella C:\Programmi\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE.  
  
2.  Digitare **Microsoft.AnalysisServices.Deployment.exe** seguito dalle opzioni corrispondenti alla modalità in cui si desidera eseguire la procedura guidata.  
  
## <a name="see-also"></a>Vedi anche  
 [Informazioni sullo script di distribuzione Analysis Services](understanding-the-analysis-services-deployment-script.md)   
 [Deploy Model Solutions Using the Deployment Wizard](deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
