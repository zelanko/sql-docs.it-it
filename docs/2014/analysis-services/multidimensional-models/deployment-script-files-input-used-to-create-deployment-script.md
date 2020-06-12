---
title: Informazioni sui file di input utilizzati per creare lo script di distribuzione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], input files
- Analysis Services Deployment Wizard, input files
- scripts [Analysis Services], deployment
- Analysis Services deployments, input files
- modifying input files
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2eb377b29ef798b4cbdd02666b866c52eb8f8599
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546876"
---
# <a name="understanding-the-input-files-used-to-create-the-deployment-script"></a>Informazioni sui file di input utilizzati per creare uno script di distribuzione
  Quando si compila un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] genera file XML per il progetto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] inserisce questi file XML nella cartella di output del progetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per impostazione predefinita l'output è situato nella cartella \Bin. Nella tabella seguente vengono elencati i file XML creati da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
|File XMLA|Descrizione|  
|---------------|-----------------|  
|\<*project name*>. asdatabase|Contiene le definizioni dichiarative per tutti gli oggetti [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contenuti nel progetto.|  
|\<*project name*>. deploymenttargets|Contiene il nome dell'istanza [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e del database in cui verranno creati gli oggetti [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|\<*project name*>. configsettings|Contiene le impostazioni specifiche all'ambiente, quali le informazioni sulla connessione all'origine dati e i percorsi di archiviazione degli oggetti. Le impostazioni in questo file eseguono l'override delle impostazioni nel \<*project name*> file con estensione asdatabase.|  
|\<*project name*>. deploymentoptions|Contiene le opzioni di distribuzione, come ad esempio se la distribuzione è transazionale o se gli oggetti distribuiti vanno elaborati dopo la distribuzione.|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] non archivia mai le password nei file di progetto.  
  
## <a name="modifying-the-input-files"></a>Modifica del file di input  
 Se si modificano i valori nei file di input o i valori recuperati dai file di input, è possibile modificare la destinazione della distribuzione, le impostazioni di configurazione e le opzioni di distribuzione senza modificare l'intero \<*project name*> file asdatabase (o un intero file di script XMLA se si genera uno script da un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database esistente). La possibilità di modificare singoli file facilita la creazione di script di distribuzione diversi per vari scopi.  
  
 Gli argomenti seguenti illustrano come modificare valori nei vari file di input:  
  
-   [Impostazione della destinazione di installazione](deployment-script-files-specifying-the-installation-target.md)  
  
-   [Impostazione delle opzioni di distribuzione dei ruoli e delle partizioni](deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [Definizione delle impostazioni di configurazione per la distribuzione di soluzioni](deployment-script-files-solution-deployment-config-settings.md)  
  
-   [Impostazione delle opzioni di elaborazione](deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione della distribuzione guidata Analysis Services](running-the-analysis-services-deployment-wizard.md)   
 [Informazioni sullo script di distribuzione di Analysis Services](understanding-the-analysis-services-deployment-script.md)  
  
  
