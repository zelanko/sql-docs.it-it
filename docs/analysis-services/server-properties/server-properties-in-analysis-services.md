---
title: Proprietà server in Analysis Services | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ce74bb210e3d5d3cd01120b0bd406672db6dd5ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207959"
---
# <a name="server-properties-in-analysis-services"></a>Proprietà server in Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Un amministratore di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] può modificare le proprietà di configurazione del server predefinite di un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Ogni istanza ha proprietà di configurazione proprie, impostate in modo indipendente rispetto ad altre istanze presenti nello stesso server.  
  
 Per configurare il server, utilizzare SQL Server Management Studio oppure modificare il file msmdsrv. ini di un'istanza specifica di SQL Server Analysis Services.  
 
Le pagine delle proprietà di SQL Server Management Studio mostrano un subset di proprietà che hanno maggiori probabilità di essere modificate. L'elenco completo delle proprietà è disponibile nel file msmdsrv.ini.   
  
> [!NOTE]  
>  In un'installazione di SQL Server Analysis Services predefinita, msmdsrv. ini è reperibile in \Programmi\Microsoft SQL Server\MSAS13. Cartella MSSQLSERVER\OLAP\Config.
> 
> Altre proprietà in grado di influenzare la configurazione del server includono le proprietà di distribuzione della configurazione riportate in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Per altre informazioni su queste proprietà, vedere [Definizione delle impostazioni di configurazione per la distribuzione di soluzioni](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md).
 
## <a name="configure-properties-in-management-studio"></a>Configurare le proprietà in Management Studio 
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2. In Esplora oggetti di fare clic con il pulsante destro del mouse sull'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e quindi scegliere **Proprietà**. Viene visualizzata la pagina Generale con le proprietà più di uso comune.  

3.  Per visualizzare proprietà aggiuntive, selezionare la casella di controllo **Mostra proprietà avanzate** nella parte inferiore della pagina.  
  
     La modifica delle proprietà del server è supportata solo per i server in modalità tabulare e multidimensionale. Se è stato installato [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], usare sempre i valori predefiniti, a meno che il supporto tecnico Microsoft non fornisca istruzioni diverse.  
  
  
## <a name="configure-properties-in-msmdsrvini"></a>Configurare le proprietà nel file msmdsrv.ini
  
Alcune proprietà possono essere impostate solo nel file msmdsrv.ini. Queste proprietà non si applicano ad Azure Analysis Services.
Se la proprietà che si desidera impostare non è visibile anche dopo aver visualizzato le proprietà avanzate, potrebbe essere necessario modificare direttamente il file msmdsrv.ini. 
  
1.  Controllare la proprietà **DataDir** nella pagina delle proprietà Generale di Management Studio per verificare il percorso dei file di programma di Analysis Services, incluso il file msmdsrv.ini.

     Su un server con più istanze, la verifica del percorso del file di programma consente di determinare se si sta modificando il file corretto.  
  
2.  Passare alla cartella **config** del percorso cartella dei file di programma.

3. Creare un backup del file nel caso sia necessario ripristinare il file originale.  
  
4.  Utilizzare un editor di testo per visualizzare o modificare il file msmdsrv.ini.  
  
5.  Salvare il file e riavviare il servizio.  
  
##  <a name="server-property-reference"></a>Guida di riferimento alle proprietà del server  
  
 Gli argomenti seguenti descrivono le varie proprietà di configurazione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] :  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Proprietà generali](../../analysis-services/server-properties/general-properties.md)|Le proprietà generali comprendono proprietà di base e proprietà avanzate, comprese le proprietà che consentono di definire la directory dei dati, la directory di backup e altre caratteristiche di funzionamento del server.|  
|[Proprietà di data mining](../../analysis-services/server-properties/data-mining-properties.md)|Le proprietà di data mining controllano quali algoritmi di data mining vengono abilitati e quali disabilitati. Per impostazione predefinita, tutti gli algoritmi sono abilitati.| 
|[Proprietà DAX](../../analysis-services/server-properties/dax-properties.md)|Definisce le proprietà correlate alle query DAX.|
|DSO|DSO non è più supportato. Le proprietà DSO vengono ignorate.|  
|[Proprietà di funzionalità](../../analysis-services/server-properties/feature-properties.md)|Le proprietà di funzionalità controllano le funzionalità di un prodotto e nella maggior parte dei casi si tratta di proprietà avanzate, comprese le proprietà che controllano i collegamenti tra istanze di server.|  
|[Proprietà della cache dei file](../../analysis-services/server-properties/filestore-properties.md)|Le proprietà di archiviazione di file sono riservate ad utenti esperti. Queste proprietà comprendono le impostazioni avanzate di gestione della memoria.|  
|[Proprietà di Gestione blocchi](../../analysis-services/server-properties/lock-manager-properties.md)|Le proprietà di gestione dei blocchi consentono di definire il comportamento del server in relazione a blocchi e timeout. La maggior parte di queste proprietà è riservata ad utenti esperti.|  
|[Proprietà dei log](../../analysis-services/server-properties/log-properties.md)|Le proprietà di registrazione controllano se, dove e come vengono registrati gli eventi sul server. Queste proprietà riguardano anche la registrazione degli errori, delle eccezioni e delle query, l'utilità Traccia eventi e le tracce.|  
|[Proprietà della memoria](../../analysis-services/server-properties/memory-properties.md)|Le proprietà della memoria controllano come il server utilizza la memoria. Queste proprietà sono destinate principalmente ad utenti esperti.|  
|[Proprietà di rete](../../analysis-services/server-properties/network-properties.md)|Le proprietà di rete controllano il comportamento del server in relazione alle reti, comprese le proprietà che controllano la compressione e l'XML binario. La maggior parte di queste proprietà è riservata ad utenti esperti.|  
|[Proprietà OLAP](../../analysis-services/server-properties/olap-properties.md)|Le proprietà OLAP controllano l'elaborazione delle dimensioni e del cubo, l'elaborazione lenta, la memorizzazione dei dati nella cache e il comportamento delle query. Comprendono sia proprietà di base che proprietà avanzate.|  
|[Proprietà di sicurezza](../../analysis-services/server-properties/security-properties.md)|La sezione sulla sicurezza comprende proprietà di base e proprietà avanzate che consentono di definire le autorizzazioni di accesso. Comprendono anche proprietà riguardanti amministratori ed utenti.|  
|[Proprietà dei pool di thread](../../analysis-services/server-properties/thread-pool-properties.md)|Le proprietà di pooling dei thread controllano il numero di thread creati dal server. Queste proprietà sono destinate principalmente ad utenti esperti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di un'istanza di Analysis Services](../../analysis-services/instances/analysis-services-instance-management.md)   
 [Definizione delle impostazioni di configurazione per la distribuzione di soluzioni](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
