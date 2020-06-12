---
title: Impostazione delle opzioni di distribuzione di partizioni e ruoli | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- partitions [Analysis Services], deployment options
- Analysis Services deployments, roles
- Analysis Services deployments, partitions
- Analysis Services Deployment Wizard, roles
- Analysis Services Deployment Wizard, partitions
- deploying [Analysis Services], roles
- roles [Analysis Services], deployment options
- deploying [Analysis Services], partitions
- modifying role deployments
- modifying partition deployments
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
author: minewiskan
ms.author: owend
ms.openlocfilehash: f4f2f5bb2f3f39636541d5aea5b931b1dcc72534
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546863"
---
# <a name="specifying-partition-and-role-deployment-options"></a>Impostazione delle opzioni di distribuzione dei ruoli e delle partizioni
  La [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuzione guidata legge le opzioni di distribuzione delle partizioni e dei ruoli dal \<*project name*> file con estensione deploymentoptions. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]crea questo file quando si compila il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Usa le opzioni di distribuzione dei ruoli e delle partizioni del progetto corrente quando \<*project name*> viene creato il file con estensione deploymentoptions. Per altre informazioni sulle impostazioni di configurazione, vedere [Informazioni sui file di input utilizzati per creare uno script di distribuzione](deployment-script-files-input-used-to-create-deployment-script.md).  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>Esame delle opzioni di distribuzione dei ruoli e delle partizioni  
 Di seguito sono riportate le opzioni di distribuzione del \<*project name*> file con estensione deploymentoptions:  
  
 **Opzioni di distribuzione delle partizioni**  
 Il \<*project name*> file con estensione deploymentoptions specifica se le partizioni esistenti nel database di destinazione vengono mantenute o sovrascritte (impostazione predefinita). Se le partizioni esistenti vengono mantenute, verranno distribuite solo le nuove partizioni, e le partizioni e le progettazioni delle aggregazioni in tutti i gruppi di misure esistenti non saranno modificate.  
  
> [!NOTE]  
>  Se il gruppo di misure contenente la partizione viene eliminato, la partizione viene eliminata automaticamente.  
  
 **Opzioni di distribuzione dei ruoli**  
 Il \<*project name*> file con estensione deploymentoptions specifica una delle opzioni di distribuzione dei ruoli seguenti:  
  
-   I ruoli e i membri di ruolo esistenti contenuti nel database di destinazione vengono mantenuti e vengono distribuiti solo i nuovi ruoli e membri di ruolo.  
  
-   Tutti i membri e ruoli esistenti contenuti nel database di destinazione vengono sostituiti dai ruoli e dai membri distribuiti.  
  
-   I ruoli e i membri di ruolo esistenti contenuti nel database di destinazione vengono mantenuti e non viene distribuito nessun nuovo ruolo.  
  
-   **Nota** Quando vengono mantenuti i ruoli e i membri esistenti, le autorizzazioni associate a tali ruoli vengono reimpostate su nessuna autorizzazione. Le autorizzazioni di sicurezza sono contenute negli oggetti da esse protetti, non nei ruoli di sicurezza a cui sono associate. Per ulteriori informazioni su come utilizzare questo comportamento utilizzando la distribuzione guidata Analysis Services, vedere "Mantieni ruoli e membri" nella Microsoft Knowledge base.  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>Modifica delle opzioni di distribuzione dei ruoli e delle partizioni  
 Potrebbe essere necessario distribuire il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto utilizzando diverse opzioni di partizione e ruolo rispetto a quelle archiviate nel \<*project name*> file con estensione deploymentoptions. È possibile, ad esempio, mantenere le partizioni, i ruoli e i membri del ruolo esistenti, anziché sostituire tutte le partizioni, i ruoli e i membri esistenti, come indicato nel \<*project name*> file con estensione deploymentoptions.  
  
 Per modificare la distribuzione di partizioni e ruoli in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto, non è possibile modificare le impostazioni delle partizioni e dei ruoli all'interno del progetto perché nella finestra *\<project name>* di dialogo **pagine delle proprietà** di non vengono [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] visualizzate tali opzioni. Se si desidera modificare le opzioni di distribuzione per ruoli e partizioni, è necessario modificare queste informazioni all'interno del \<*project name*> file con estensione deploymentoptions. Nella procedura seguente viene descritto come modificare le opzioni di distribuzione di partizioni e ruoli all'interno del \<*project name*> file con estensione deploymentoptions.  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>Per modificare la distribuzione delle partizioni o dei ruoli dopo la generazione dei file di input  
  
-   Eseguire Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modo interattivo e specificare nuove opzioni di distribuzione delle partizioni e dei ruoli nella pagina relativa alle **opzioni partizioni e ruoli della distribuzione** .  
  
     -oppure-  
  
-   Eseguire Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] attraverso il prompt dei comandi e impostarla in modo che venga eseguita in modalità file di risposte. Per ulteriori informazioni sulla modalità file di risposte, vedere [esecuzione della distribuzione guidata Analysis Services](running-the-analysis-services-deployment-wizard.md).  
  
     -oppure-  
  
-   Aprire il \<*project name*> deploymentoptions in qualsiasi editor di testo e modificare manualmente le opzioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostazione della destinazione di installazione](deployment-script-files-specifying-the-installation-target.md)   
 [Specifica delle impostazioni di configurazione per la distribuzione della soluzione](deployment-script-files-solution-deployment-config-settings.md)   
 [Impostazione delle opzioni di elaborazione](deployment-script-files-specifying-processing-options.md)  
  
  
