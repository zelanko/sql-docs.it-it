---
title: Creazione di progetti di Analysis Services (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Analysis Services], building
- Business Intelligence Development Studio, project building [Analysis Services]
ms.assetid: caac03cb-b2b4-4652-8913-3dd39c4b0127
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97e32b80d19675b3763101d1c226529a48e23e68
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66076776"
---
# <a name="build-analysis-services-projects-ssdt"></a>Compilare progetti di Analysis Services (SSDT)
  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]la compilazione di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è molto simile alla compilazione di qualsiasi progetto di programmazione in Visual Studio. Quando si compila il progetto, nella directory di output viene creato un set di file XML. Questi file XML sono basati su Analysis Services Scripting Language (ASSL), il sottolinguaggio XML utilizzato dalle applicazioni client come [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per comunicare con un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] allo scopo di creare o modificare oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Questi file XML permettono di distribuire definizioni di oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un'istanza specificata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="building-a-project"></a>Compilazione di un progetto  
 Quando si compila un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] viene compilato un set completo di file XML nella cartella di output con tutti i comandi ASSL necessari per compilare tutti gli oggetti di database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nel progetto. Se il progetto è stato compilato in precedenza ed è stata specificata la distribuzione incrementale per la configurazione attiva, in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] viene inoltre compilato un file XML contenente i comandi ASSL per l'esecuzione di un aggiornamento incrementale agli oggetti distribuiti. Questo file XML viene scritto nella cartella ..\obj\\\<configurazione attiva>\> del progetto. Le compilazioni incrementali consentono un risparmio di tempo in caso di distribuzione ed elaborazione di un database o un progetto di dimensioni estremamente elevate.  
  
> [!NOTE]  
>  Il comando Ricompila tutto consente di ignorare l'impostazione relativa alla distribuzione incrementale.  
  
 La compilazione di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina la convalida delle definizioni di oggetti nel progetto. La convalida include qualsiasi assembly a cui viene fatto riferimento. Gli errori di compilazione vengono visualizzati nella finestra Elenco attività, con il testo dell'errore della libreria AMO (Analysis Management Objects). È possibile fare clic su un errore per aprire la finestra di progettazione necessaria per la relativa correzione.  
  
 L'esito positivo della convalida non garantisce la possibilità di creare gli oggetti sul server di destinazione durante la distribuzione o di elaborarli correttamente in seguito. I problemi seguenti possono impedire la corretta esecuzione della distribuzione o dell'elaborazione dopo la distribuzione:  
  
-   Non vengono eseguiti controlli di sicurezza per il server e la distribuzione può pertanto essere impedita da blocchi.  
  
-   I percorsi fisici non vengono convalidati sul server.  
  
-   I dettagli delle viste origine dati non vengono controllati rispetto all'origine dei dati effettiva sul server di destinazione.  
  
 Se la convalida ha esito positivo, in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] vengono generati i file XML. Al termine della compilazione, la cartella di output contiene i file descritti nella tabella seguente.  
  
|File (nella cartella bin)|Descrizione|  
|-----------------------------|-----------------|  
|*Nomeprogetto*.asdatabase|Contiene gli elementi ASSL che definiscono i metadati per gli oggetti nel progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] all'interno di un file di script di distribuzione. Questo file viene usato dal motore di distribuzione per distribuire gli oggetti in un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|*Nomeprogetto*.configsettings|Contiene le impostazioni di configurazione usate durante la distribuzione, che possono essere modificate direttamente oppure usando la Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ad esempio, la stringa di connessione per le origini dati).|  
|*Nomeprogetto*.deploymenttargets|Contiene le impostazioni relative alla destinazione utilizzate durante la distribuzione, modificabili direttamente oppure nella Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ad esempio, i nomi di server e database).|  
|*Nomeprogetto*.deploymentoptions|Contiene diverse impostazioni di opzioni usate durante la distribuzione, che possono essere modificate direttamente oppure usando la Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ad esempio, i percorsi di archiviazione).|  
|*AssemblyName*/*dllname.* dll|Cartelle separate per ogni assembly a cui viene fatto riferimento, ognuna delle quali contiene la DLL per l'assembly, qualsiasi assembly di riferimento e qualsiasi file con estensione pdb associato per le informazioni di debug dell'output.|  
  
|File (nella cartella obj)|Descrizione|  
|-----------------------------|-----------------|  
|\<Nome configurazione> \LastBuilt.xml|Contiene il timestamp e il codice hash che identificano l'ultima compilazione del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
 Questi file XML non contengono \<i tag create> \<e alter>, che vengono costruiti durante la distribuzione.  
  
 Nella directory di output vengono inoltre copiati gli assembly a cui viene fatto riferimento, ad eccezione degli assembly di sistema standard e di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . In presenza di riferimenti ad altri progetti di una soluzione, tali progetti vengono innanzitutto compilati, utilizzando la configurazione di progetto appropriata e le dipendenze di compilazione stabilite dai riferimenti ai progetti, e quindi copiati nella cartella di output del progetto.  
  
## <a name="see-also"></a>Vedi anche  
 [Analysis Services linguaggio di scripting &#40;riferimento&#41; ASSL](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [Distribuire progetti di Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
