---
title: Impostazione opzioni di distribuzione dei ruoli e delle partizioni | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8bd62cc5fef3ef13dede85c06b28b0501a83de2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178450"
---
# <a name="deployment-script-files---partition-and-role-deployment-options"></a>File di script di distribuzione - Opzioni di distribuzione dei ruoli e delle partizioni
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuzione guidata di legge le opzioni di distribuzione di ruoli e delle partizioni dal \< *nome del progetto*>. deploymentoptions file. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea questo file quando si compila il progetto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Usa le opzioni di distribuzione di ruoli e delle partizioni dell'oggetto corrente progetto quando il \< *nome progetto*>. deploymentoptions file viene creato. Per altre informazioni sulle impostazioni di configurazione, vedere [Informazioni sui file di input utilizzati per creare uno script di distribuzione](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md).  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>Esame delle opzioni di distribuzione dei ruoli e delle partizioni  
 Lle opzioni di distribuzione nel \< *nome progetto*>. deploymentoptions file includono quanto segue:  
  
 **Opzioni di distribuzione delle partizioni**  
 Il \< *nome progetto*>. deploymentoptions file specifica se le partizioni esistenti nel database di destinazione vengono mantenute o vengono sovrascritte (impostazione predefinita). Se le partizioni esistenti vengono mantenute, verranno distribuite solo le nuove partizioni, e le partizioni e le progettazioni delle aggregazioni in tutti i gruppi di misure esistenti non saranno modificate.  
  
> [!NOTE]  
>  Se il gruppo di misure contenente la partizione viene eliminato, la partizione viene eliminata automaticamente.  
  
 **Opzioni di distribuzione dei ruoli**  
 Il \< *nome progetto*>. deploymentoptions file viene specificata una delle seguenti opzioni di distribuzione ruolo:  
  
-   I ruoli e i membri di ruolo esistenti contenuti nel database di destinazione vengono mantenuti e vengono distribuiti solo i nuovi ruoli e membri di ruolo.  
  
-   Tutti i membri e ruoli esistenti contenuti nel database di destinazione vengono sostituiti dai ruoli e dai membri distribuiti.  
  
-   I ruoli e i membri di ruolo esistenti contenuti nel database di destinazione vengono mantenuti e non viene distribuito nessun nuovo ruolo.  
  
-   **Nota** Quando vengono mantenuti i ruoli e i membri esistenti, le autorizzazioni associate a tali ruoli vengono reimpostate su nessuna autorizzazione. Le autorizzazioni di sicurezza sono contenute negli oggetti da esse protetti, non nei ruoli di sicurezza a cui sono associate. Per altre informazioni sull'utilizzo di questo comportamento con la distribuzione guidata Analysis Services, vedere "Mantieni ruoli e membri" nella Microsoft Knowledge Base.  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>Modifica delle opzioni di distribuzione dei ruoli e delle partizioni  
 Potrebbe essere necessario distribuire il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del progetto usando opzioni per ruoli e partizioni diverse da quelle archiviate nel \< *nome del progetto*>. deploymentoptions file. Ad esempio, si desidera mantenere le partizioni esistenti, i ruoli e i membri del ruolo, invece che sostituire tutte le partizioni esistenti, i ruoli e membri come indicato nella \< *nome progetto*>. deploymentoptions file.  
  
 Per modificare la distribuzione di partizioni e ruoli in un' [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto, non è possibile modificare le impostazioni di partizioni e dei ruoli all'interno del progetto perché il  *\<nome progetto >* **le pagine delle proprietà**  nella finestra di dialogo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] queste opzioni non sono visualizzate. Se si desidera modificare le opzioni di distribuzione per i ruoli e partizioni, è necessario modificare queste informazioni all'interno di \< *nome progetto*>. deploymentoptions stesso file. La procedura seguente viene descritto come modificare le opzioni di distribuzione di ruoli e partizioni entro il \< *nome progetto*>. deploymentoptions file.  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>Per modificare la distribuzione delle partizioni o dei ruoli dopo la generazione dei file di input  
  
-   Eseguire Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modo interattivo e specificare nuove opzioni di distribuzione delle partizioni e dei ruoli nella pagina relativa alle **opzioni partizioni e ruoli della distribuzione** .  
  
     -oppure-  
  
-   Eseguire Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] attraverso il prompt dei comandi e impostarla in modo che venga eseguita in modalità file di risposte. Per altre informazioni sulla modalità file di risposte, vedere [Esecuzione della Distribuzione guidata Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     -oppure-  
  
-   Aprire il \< *nome progetto*>. deploymentoptions in un editor di testo e manualmente modificare le opzioni. Le opzioni per PartitionDeployment sono DeployPartitions, RetainPartitions. Le opzioni per RoleDeployment sono DeployRolesAndMembers, DeployRolesRetainMembers, RetainRoles.
  
## <a name="see-also"></a>Vedere anche  
 [Impostazione della destinazione di installazione](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [Definizione delle impostazioni di configurazione per la distribuzione di soluzioni](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)   
 [Impostazione delle opzioni di elaborazione](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  
