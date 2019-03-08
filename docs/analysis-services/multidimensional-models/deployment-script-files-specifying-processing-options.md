---
title: Specifica le opzioni di elaborazione | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54be969446b9c1b234860ce2a68c1208634246ce
ms.sourcegitcommit: d6ef87a01836738b5f7941a68ca80f98c61a49d4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57572774"
---
# <a name="deployment-script-files---specifying-processing-options"></a>File di Script di distribuzione - specificare le opzioni di elaborazione
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuzione guidata di legge le opzioni di elaborazione dal \< *nome del progetto*>. deploymentoptions file. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea questo file quando si compila il progetto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Usa le opzioni di elaborazione specificate sulla **distribuzione** pagina della  *\<nome progetto >* **le pagine delle proprietà** finestra di dialogo per creare il \< *nome progetto*>. deploymentoptions file.  
  
## <a name="reviewing-the-processing-options-for-deployment"></a>Esame delle opzioni di elaborazione per la distribuzione  
 Le impostazioni di configurazione archiviate all'interno di \< *nome progetto*>. deploymentoptions file sono i seguenti:  
  
-   **Metodo di elaborazione** Questa impostazione determina se gli oggetti distribuiti vengono elaborati dopo la distribuzione e il tipo di elaborazione a cui verranno sottoposti. Sono previste tre opzioni di elaborazione:  
  
    -   Elaborazione predefinita (impostazione predefinita) rileva lo stato di elaborazione di oggetti di database ed esegue l'elaborazione necessaria per restituire oggetti non elaborati o elaborati parzialmente in uno stato completamente elaborato.
  
    -   L'elaborazione completa elabora un oggetto e tutti gli oggetti in esso contenuti. Quando viene eseguita l'elaborazione completa su un oggetto che è già stato elaborato, questa operazione viene completata solo dopo che sono stati eliminati tutti i dati contenuti nell'oggetto. 
  
    -   None indica che non viene eseguita alcuna elaborazione.


-   **Opzioni tabella writeback** Se il writeback è attivato nel progetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , questa impostazione stabilisce come verrà gestito. Sono previste tre opzioni per la tabella writeback:  
  
    -   Per impostazione predefinita, se esiste una tabella writeback essa verrà utilizzata. Se non esiste alcuna tabella writeback, ne verrà creata una nuova.  
  
    -   Se la tabella writeback esiste già, non potrà essere portata a termine la distribuzione. Se non esiste alcuna tabella writeback, ne verrà creata una nuova.  
  
    -   Anche se dovesse esistere già una tabella writeback, ne verrà creata una nuova. In questo caso, Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elimina ogni eventuale tabella esistente e la sostituisce con una nuova tabella writeback.  
  
-   **Distribuzione transazionale** Questa impostazione stabilisce se la distribuzione delle modifiche dei metadati e dei comandi di elaborazione viene eseguita attraverso una singola transazione o in transazioni separate.  
  
    -   Se questa opzione è impostata su **True** (impostazione predefinita), [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuisce tutte le modifiche dei metadati e tutti i comandi di elaborazione attraverso una singola transazione.  
  
    -   Se invece questa opzione è impostata su **False**, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuisce le modifiche dei metadati attraverso una singola transazione e distribuisce ogni comando di elaborazione in transazioni separate.  
  
## <a name="modifying-the-processing-options-for-deployment"></a>Modifica delle opzioni di elaborazione per la distribuzione  
 Tuttavia, potrebbe essere necessario distribuire il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del progetto usando opzioni di elaborazione diverse da quelle archiviate nel \< *nome del progetto*>. deploymentoptions file. Potrebbe ad esempio essere preferibile elaborare tutti gli oggetti in modo completo o elaborarli utilizzando l'opzione di elaborazione predefinita o infine non elaborarli affatto. Se i cubi o le dimensioni sono abilitati per la scrittura, è possibile specificare se verrà utilizzata una tabella writeback nuova o preesistente.  
  
 Per modificare le opzioni di elaborazione da utilizzare durante la distribuzione, è possibile modificare o ricompilare il progetto, oppure è possibile modificare le opzioni di elaborazione nel file di input utilizzando uno dei metodi descritti nella procedura seguente.  
  
#### <a name="to-change-processing-options-after-the-input-files-have-been-generated"></a>Per modificare le opzioni di elaborazione dopo la generazione dei file di input  
  
-   Eseguire Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modo interattivo. Nella pagina **Opzioni di elaborazione** specificare le opzioni di elaborazione per il progetto da distribuire.  
  
     oppure  
  
-   Eseguire Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] attraverso il prompt dei comandi e impostarla in modo che venga eseguita in modalità file di risposte. Per altre informazioni sulla modalità file di risposte, vedere [Esecuzione della Distribuzione guidata Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     oppure  
  
-   Modificare il \< *nome progetto*>. deploymentoptions file utilizzando un editor di testo.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostazione della destinazione di installazione](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [Impostazione delle opzioni di distribuzione dei ruoli e delle partizioni](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [Definizione delle impostazioni di configurazione per la distribuzione di soluzioni](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
