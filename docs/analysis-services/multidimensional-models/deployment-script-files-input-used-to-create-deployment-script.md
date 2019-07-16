---
title: Informazioni sui file di Input utilizzati per creare lo Script di distribuzione | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b75ec5d7433931a81a0fa6e2c648f85335fbedc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208973"
---
# <a name="deployment-script-files---input-used-to-create-deployment-script"></a>File di Script di distribuzione - Input usato per creare Script di distribuzione
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Quando si compila un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] genera file del progetto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] inserisce questi file nella cartella di Output del [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto. Per impostazione predefinita l'output è situato nella cartella \Bin. Nella tabella seguente vengono elencati i file XML creati da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
|File|Descrizione|  
|---------------|-----------------|  
|\<*nome del progetto*>. asdatabase|Un file XMLA per progetti di modello tabulare 1100 o 1103 o multidimensionale, o un file JSON per tabulare 1200 e superiore progetti di modello. Contiene le definizioni dichiarative per tutti gli oggetti [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contenuti nel progetto.|  
|\<*nome del progetto*>. deploymenttargets|Contiene il nome dell'istanza [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e del database in cui verranno creati gli oggetti [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|\<*nome del progetto*>. configsettings|Contiene le impostazioni specifiche all'ambiente, quali le informazioni sulla connessione all'origine dati e i percorsi di archiviazione degli oggetti. Le impostazioni in questo file sostituiscono le impostazioni nel \< *nome progetto*> file con estensione asdatabase.|  
|\<*nome del progetto*>. deploymentoptions|Contiene le opzioni di distribuzione, come ad esempio se la distribuzione è transazionale o se gli oggetti distribuiti vanno elaborati dopo la distribuzione.|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] non archivia mai le password nei file di progetto.  
  
## <a name="modifying-the-input-files"></a>Modifica del file di input  
 Modificando i valori nei file di input o i valori recuperati dai file di input, è possibile modificare la destinazione di distribuzione, le impostazioni di configurazione e le opzioni di distribuzione senza dover modificare l'intero \< *progetto nome*> file con estensione asdatabase (o un intero file di script se si genera uno script da un oggetto esistente [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database). La possibilità di modificare singoli file facilita la creazione di script di distribuzione diversi per vari scopi.  
  
 Gli argomenti seguenti illustrano come modificare valori nei vari file di input:  
  
-   [Impostazione della destinazione di installazione](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)  
  
-   [Impostazione delle opzioni di distribuzione dei ruoli e delle partizioni](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [Definizione delle impostazioni di configurazione per la distribuzione di soluzioni](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
-   [Impostazione delle opzioni di elaborazione](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione della Distribuzione guidata Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Informazioni sullo script di distribuzione di Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  
