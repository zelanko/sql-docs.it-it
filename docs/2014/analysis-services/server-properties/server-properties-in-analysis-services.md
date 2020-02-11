---
title: Configurare le proprietà del server in Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, configuration properties
- Analysis Services, configuration properties
- SQL Server Analysis Services, configuration properties
- configuration options [Analysis Services]
- server properties [Analysis Services]
- properties [Analysis Services], configuration
- properties [Analysis Services]
ms.assetid: 274b89cd-14ed-4666-bc13-eedf1de51e18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 31c05bbc1be8376144eb191ff28a9cdc6eebdd8a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068896"
---
# <a name="configure-server-properties-in-analysis-services"></a>Configurare le proprietà del server in Analysis Services
  Un amministratore di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] può modificare le proprietà di configurazione del server predefinite per un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Ogni istanza ha proprietà di configurazione proprie che è possibile impostare in modo indipendente rispetto ad altre istanze nello stesso server.  
  
 Per impostare le proprietà del server, utilizzare SQL Server Management Studio oppure modificare il file msmdsrv.ini di un'istanza specifica.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Configurare le proprietà del server (istanza)](#bkmk_config)  
  
 [Riferimento alle proprietà del server](#bkmk_ref)  
  
##  <a name="bkmk_config"></a>Configurare le proprietà del server (istanza)  
 La pagina delle proprietà in SQL Server Management Studio contiene un subset delle proprietà disponibili e consente di visualizzare solo le proprietà la cui modifica è più probabile. Il set completo delle proprietà è disponibile nel file msmdsrv.ini.  
  
> [!NOTE]  
>  In questo argomento non sono documentate le proprietà di configurazione della distribuzione in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Per ulteriori informazioni sulla configurazione della distribuzione, vedere [specifica delle impostazioni di configurazione per la distribuzione della soluzione](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md).  
  
#### <a name="view-or-set-configuration-properties-in-management-studio"></a>Visualizzare o impostare le proprietà di configurazione in Management Studio  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
     In Esplora oggetti di fare clic con il pulsante destro del mouse sull'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e quindi scegliere **Proprietà**. Viene visualizzata la pagina Generale con le proprietà più di uso comune.  
  
2.  Per visualizzare proprietà aggiuntive, selezionare la casella di controllo **Mostra proprietà avanzate** nella parte inferiore della pagina.  
  
     La modifica delle proprietà del server è supportata solo per i server in modalità tabulare e multidimensionale. Se è stato installato [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], utilizzare sempre i valori predefiniti, a meno che vengano fornite istruzioni diverse da un addetto del supporto tecnico Microsoft.  
  
     Per informazioni su come risolvere problemi operativi o riguardanti le prestazioni usando le proprietà del server, vedere la Guida operativa di [SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
     Per ottenere informazioni sulle proprietà del server, molte delle quali sono rimaste invariate rispetto alle diverse versioni precedenti, leggere il white paper Microsoft [Proprietà server di SQL Server 2005 Analysis Services (SSAS)](https://go.microsoft.com/fwlink/?LinkID=199102).  
  
    > [!NOTE]  
    >  Alcune proprietà possono essere impostate solo nel file msmdsrv.ini. Se la proprietà che si desidera impostare non è visibile anche dopo aver visualizzato le proprietà avanzate, potrebbe essere necessario modificare direttamente il file msmdsrv.ini.  
  
#### <a name="view-or-edit-configuration-properties-in-the-msmdsrvini-file"></a>Visualizzare o modificare manualmente le proprietà di configurazione nel file msmdsrv.ini  
  
1.  Prima di iniziare, controllare la proprietà **DATADIR** nella pagina delle proprietà generale di Management Studio per verificare il percorso dei file di programma Analysis Services, incluso il file msmdsrv. ini. La verifica del percorso dei file di programma consente di determinare se si stia modificando il file corretto.  
  
    > [!NOTE]  
    >  In un'installazione predefinita, il file si trova nella cartella \Programmi\Microsoft SQL Server\MSAS12.MSSQLSERVER\OLAP\Config.  
  
2.  Creare un backup del file nel caso sia necessario ripristinare il file originale.  
  
3.  Utilizzare un editor di testo per visualizzare o modificare il file msmdsrv.ini.  
  
4.  Dopo aver salvato il file, è necessario riavviare il servizio.  
  
##  <a name="bkmk_ref"></a>Riferimento alle proprietà del server  
 Le proprietà di configurazione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono importanti per ottimizzare il proprio sistema. È ad esempio possibile impostare particolari proprietà per fare in modo che il log delle query funzioni in conformità ai propri requisiti.  
  
 Negli argomenti seguenti vengono descritte le varie proprietà di configurazione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Proprietà generali](general-properties.md)|Le proprietà generali comprendono proprietà di base e proprietà avanzate, comprese le proprietà che consentono di definire la directory dei dati, la directory di backup e altre caratteristiche di funzionamento del server.|  
|[Proprietà di data mining](data-mining-properties.md)|Le proprietà di data mining controllano quali algoritmi di data mining vengono abilitati e quali disabilitati. Per impostazione predefinita, tutti gli algoritmi sono abilitati.|  
|DSO|DSO non è più supportato. Le proprietà DSO vengono ignorate.|  
|[Proprietà di funzionalità](feature-properties.md)|Le proprietà di funzionalità controllano le funzionalità di un prodotto e nella maggior parte dei casi si tratta di proprietà avanzate, comprese le proprietà che controllano i collegamenti tra istanze di server.|  
|[FileStore - proprietà](filestore-properties.md)|Le proprietà di archiviazione di file sono riservate ad utenti esperti. Queste proprietà comprendono le impostazioni avanzate di gestione della memoria.|  
|[Proprietà di Gestione blocchi](lock-manager-properties.md)|Le proprietà di gestione dei blocchi consentono di definire il comportamento del server in relazione a blocchi e timeout. La maggior parte di queste proprietà è riservata ad utenti esperti.|  
|[Proprietà dei log](log-properties.md)|Le proprietà di registrazione controllano se, dove e come vengono registrati gli eventi sul server. Queste proprietà riguardano anche la registrazione degli errori, delle eccezioni e delle query, l'utilità Traccia eventi e le tracce.|  
|[Proprietà della memoria](memory-properties.md)|Le proprietà della memoria controllano come il server utilizza la memoria. Queste proprietà sono destinate principalmente ad utenti esperti.|  
|[Proprietà di rete](network-properties.md)|Le proprietà di rete controllano il comportamento del server in relazione alle reti, comprese le proprietà che controllano la compressione e l'XML binario. La maggior parte di queste proprietà è riservata ad utenti esperti.|  
|[Proprietà OLAP](olap-properties.md)|Le proprietà OLAP controllano l'elaborazione delle dimensioni e del cubo, l'elaborazione lenta, la memorizzazione dei dati nella cache e il comportamento delle query. Comprendono sia proprietà di base che proprietà avanzate.|  
|[Proprietà di sicurezza](security-properties.md)|La sezione sulla sicurezza comprende proprietà di base e proprietà avanzate che consentono di definire le autorizzazioni di accesso. Comprendono anche proprietà riguardanti amministratori ed utenti.|  
|[Proprietà dei pool di thread](thread-pool-properties.md)|Le proprietà di pooling dei thread controllano il numero di thread creati dal server. Queste proprietà sono destinate principalmente ad utenti esperti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione dell'istanza di Analysis Services](../instances/analysis-services-instance-management.md)   
 [Definizione delle impostazioni di configurazione per la distribuzione di soluzioni](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
