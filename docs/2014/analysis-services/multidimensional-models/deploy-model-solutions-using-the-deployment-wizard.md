---
title: Distribuire soluzioni di modelli tramite la distribuzione guidata | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard
- deploying [Analysis Services], Analysis Services Deployment Wizard
- Analysis Services deployments, Analysis Services Deployment Wizard
- Analysis Services Deployment Wizard, about Analysis Services Deployment Wizard
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e18b1786201be9ba671bc08fe7b24ba2207469e9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075383"
---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>Deploy Model Solutions Using the Deployment Wizard
  Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizza i file di output XML generati da un progetto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] come file di input. Questi file di input possono essere facilmente modificati per personalizzare la distribuzione di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Lo script di distribuzione generato può quindi essere eseguito subito oppure salvato per essere distribuito in una fase successiva.  
  
 È possibile effettuare la distribuzione utilizzando la procedura guidata come indicato in questa sezione. È anche possibile automatizzare la distribuzione o utilizzare la funzionalità di sincronizzazione. Se il database distribuito è di grandi dimensioni, è consigliabile utilizzare partizioni sui sistemi di destinazione. È inoltre possibile automatizzare il popolamento e la creazione delle partizioni utilizzando la libreria AMO (Analysis Management Objects).  
  
> [!IMPORTANT]  
>  L'ID utente e la password eventualmente specificati nella stringa di connessione per un'origine dati o ai fini della rappresentazione non sono contenuti né nei file di output XML né nello script di distribuzione. Poiché in questo scenario sono necessarie per l'elaborazione, è necessario aggiungere tali informazioni manualmente. Se la distribuzione non include l'elaborazione, è possibile aggiungere le informazioni di connessione e le impostazioni di rappresentazione in base alle esigenze dopo la distribuzione. Se la distribuzione include l'elaborazione, si possono aggiungere tali informazioni e impostazioni nella procedura guidata oppure nello script di distribuzione dopo il relativo salvataggio.  
  
## <a name="in-this-section"></a>In questa sezione  
 Gli argomenti seguenti descrivono come utilizzare Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , i file di input e lo script di distribuzione:  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Esecuzione della Distribuzione guidata Analysis Services](running-the-analysis-services-deployment-wizard.md)|Descrive i vari modi in cui si può eseguire Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Informazioni sui file di input utilizzati per creare uno script di distribuzione](deployment-script-files-input-used-to-create-deployment-script.md)|Descrive quali file vengono utilizzati da Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] come valori di input e il contenuto di ciascuno di questi file. Contiene inoltre collegamenti a vari argomenti che descrivono come modificare i valori contenuti in ciascun file di input.|  
|[Informazioni sullo script di distribuzione di Analysis Services](understanding-the-analysis-services-deployment-script.md)|Descrive il contenuto dello script di distribuzione e come viene eseguito lo script.|  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuire soluzioni di modelli utilizzando XMLA](deploy-model-solutions-using-xmla.md)   
 [Sincronizzare database di Analysis Services](synchronize-analysis-services-databases.md)   
 [Informazioni sui file di input utilizzati per creare uno script di distribuzione](deployment-script-files-input-used-to-create-deployment-script.md)   
 [Distribuire soluzioni di modelli con l'utilità di distribuzione](deploy-model-solutions-with-the-deployment-utility.md)  
  
  
