---
title: Database dell'area di lavoro (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 662daf08-a514-44a7-8675-44644aa454a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d70cf1724eb67dbf8f1a75989df5f4021b5512d6
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52416702"
---
# <a name="workspace-database-ssas-tabular"></a>Database dell'area di lavoro (SSAS tabulare)
  Il database dell'area di lavoro modello tabulare, usato durante la creazione del modello, viene creato quando si crea un nuovo progetto di modello tabulare in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Tale database risiede in memoria in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione in modalità tabulare, in genere nello stesso computer di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
-   [Panoramica del Database dell'area di lavoro](#bkmk_overview)  
  
-   [Proprietà del Database dell'area di lavoro](#bkmk_ws_prop)  
  
-   [Utilizzo di SSMS per gestire il Database dell'area di lavoro](#bkmk_use_ssms)  
  
-   [Attività correlate](#bkmk_related_tasks)  
  
##  <a name="bkmk_overview"></a> Panoramica del Database dell'area di lavoro  
 Un database dell'area di lavoro viene creato nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , specificata nella proprietà Server dell'area di lavoro, quando si crea un nuovo progetto di business intelligence tramite uno dei modelli del progetto di modello tabulare in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Ogni progetto di modello tabulare disporrà del relativo database dell'area di lavoro. È possibile utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per visualizzare il database dell'area di lavoro nel server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Nel nome del database dell'area di lavoro è incluso il nome del progetto, seguito da un carattere di sottolineatura, dal nome utente, da un carattere di sottolineatura e infine da un GUID.  
  
 Il database dell'area di lavoro si trova in memoria mentre il progetto di modello tabulare viene aperto in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Quando si chiude il progetto, il database dell'area di lavoro può essere mantenuto in memoria, archiviato su disco e rimosso dalla memoria (impostazione predefinita) o essere rimosso dalla memoria e non archiviato su disco, come determinato dalla proprietà Memorizzazione area di lavoro. Per altre informazioni sulla proprietà Memorizzazione area di lavoro, vedere le [proprietà del database dell'area di lavoro](#bkmk_ws_prop) più avanti in questo argomento.  
  
 Dopo avere aggiunto dati al progetto di modello tramite l'Importazione guidata tabella o un'operazione di copia e incolla, quando si visualizzano le tabelle, le colonne e i dati in Progettazione modelli, viene in pratica visualizzato il database dell'area di lavoro. Se si aggiungono altre tabelle, colonne, relazioni e così via, il database dell'area di lavoro viene modificato.  
  
> [!IMPORTANT]  
>  Se una tabella nel modello conterrà un numero considerevole di righe, si consideri di importare solo un subset dei dati durante la creazione di modelli. L'importazione di un subset dei dati consente di ridurre tempi di elaborazione e utilizzo delle risorse server per il database dell'area di lavoro.  
  
> [!NOTE]  
>  Nella finestra di anteprima delle finestre di dialogo Modifica proprietà tabella e Gestione partizioni della pagina Selezione tabelle e viste nell'Importazione guidata tabella vengono visualizzate tabelle, colonne e righe nell'origine dati e potrebbero non essere mostrate le stesse tabelle, colonne e righe del database dell'area di lavoro.  
  
 Quando si distribuisce un progetto di modello tabulare, il database del modello distribuito, che essenzialmente è una copia del database dell'area di lavoro, viene creato nell'istanza del server Analysis Services specificata nella proprietà Server di distribuzione. Per altre informazioni sulla proprietà Server di distribuzione, vedere [Proprietà del progetto &#40;SSAS tabulare&#41;](properties-ssas-tabular.md).  
  
 Il database dell'area di lavoro modello si trova in genere nel localhost o in un'istanza denominata locale di un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. È possibile utilizzare un'istanza remota di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per ospitare il database dell'area di lavoro, ma si tratta di una configurazione non consigliata a causa della latenza durante le query dei dati e di altre restrizioni. In modo ottimale, l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui verranno ospitati i database dell'area di lavoro si trova nello stesso computer di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. La creazione di progetti di modello nello stesso computer dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui è ospitato il database dell'area di lavoro può migliorare le prestazioni.  
  
 I database dell'area di lavoro remoti presentano le restrizioni seguenti:  
  
-   Possibile latenza durante le query.  
  
-   Non è possibile impostare la proprietà Backup dei dati sull'opzione relativa al **backup su disco**.  
  
-   Non è possibile importare dati da una cartella di lavoro di PowerPivot quando si crea un nuovo progetto di modello tabulare utilizzando il modello di progetto Importa da PowerPivot.  
  
##  <a name="bkmk_ws_prop"></a> proprietà del database dell'area di lavoro  
 Le proprietà del database dell'area di lavoro sono incluse nelle proprietà del modello. Per visualizzare le proprietà dei modelli, in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]Esplora soluzioni **di**fare clic sul file **Model.bim** . Le proprietà dei modelli possono essere configurate usando la finestra **Proprietà** . Nelle proprietà specifiche del database dell'area di lavoro è incluso quanto indicato di seguito:  
  
> [!NOTE]  
>  Le proprietà **Server dell'area di lavoro**, **Memorizzazione area di lavoro** e **Backup dei dati** dispongono di impostazioni predefinite applicate quando si crea un nuovo progetto di modello. È possibile modificare le impostazioni predefinite per nuovi progetti di modello nella pagina **Modellazione dati** nelle impostazioni di **Analysis Server** in Strumenti\finestra di dialogo Opzioni. Queste proprietà, come altre, possono essere impostate anche per ogni progetto di modello nella finestra **Proprietà** . Le modifiche apportate alle impostazioni predefinite non verranno applicate ai progetti di modello già creati. Per altre informazioni, vedere [Configurare la modellazione dei dati e le proprietà di distribuzione predefinite &#40;SSAS tabulare&#41;](configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Database dell'area di lavoro**|Nome del progetto, seguito da un carattere di sottolineatura, dal nome utente, da un carattere di sottolineatura e infine da un GUID.|Nome del database dell'area di lavoro utilizzato per l'archiviazione e la modifica del progetto di modello. Al termine della creazione di un progetto di modello tabulare, questo database verrà visualizzato nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specificata nella proprietà **Server dell'area di lavoro**. Questa proprietà non può essere impostata nella finestra Proprietà.|  
|**Memorizzazione area di lavoro**|Scarica dalla memoria|Viene specificato come viene mantenuto un database dell'area di lavoro dopo la chiusura di un progetto di modello. In un database dell'area di lavoro sono inclusi i metadati del modello e i dati importati. In alcuni casi, le dimensioni del database dell'area di lavoro possono essere elevate e utilizzare quindi una grande quantità di memoria. Per impostazione predefinita, quando si chiude un progetto di modello in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], il database dell'area di lavoro viene scaricato dalla memoria. Quando si modifica questa impostazione, è importante considerare le risorse di memoria disponibili, nonché pianificare la frequenza con la quale utilizzare il progetto di modello. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> **Mantieni in memoria** : viene specificato di mantenere il database dell'area di lavoro in memoria dopo la chiusura di un progetto di modello. Per questa opzione verrà utilizzata più memoria; tuttavia, in caso di apertura di un progetto di modello in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], vengono utilizzate meno risorse e i carichi nel database dell'area di lavoro verranno eseguiti più velocemente.<br /><br /> **Scarica dalla memoria** : viene specificato di mantenere il database dell'area di lavoro su disco, ma non più in memoria dopo la chiusura di un progetto di modello. Per questa opzione verrà usa meno memoria. Tuttavia, in caso di apertura di un progetto di modello in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], il database dell'area di lavoro deve essere collegato di nuovo. Vengono usate risorse aggiuntive e il caricamento del progetto di modello sarà più lento rispetto a quando il database dell'area di lavoro è mantenuto in memoria. Utilizzare questa opzione quando le risorse in memoria sono limitate o quando in uso in un database dell'area di lavoro remoto.<br /><br /> **Elimina area di lavoro** : viene specificato di eliminare il database dell'area di lavoro dalla memoria e di non mantenerlo su disco dopo la chiusura del progetto di modello. Per questa opzione verranno usati meno memoria e meno spazio di archiviazione. Tuttavia, in caso di apertura di un progetto di modello in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], vengono use risorse aggiuntive e il caricamento del progetto di modello sarà più lento rispetto a quando il database dell'area di lavoro è mantenuto in memoria o su disco. Utilizzare questa opzione quando i progetti di modello vengono utilizzati solo occasionalmente.<br /><br /> <br /><br /> L'impostazione predefinita per questa proprietà può essere modificata nella pagina **Modellazione dati** nelle impostazioni di **Analysis Server** in Strumenti\finestra di dialogo Opzioni.|  
|**Server dell'area di lavoro**|localhost|Questa proprietà consente di specificare il server predefinito che sarà utilizzato per ospitare il database dell'area di lavoro mentre si crea il progetto di modello in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Tutte le istanze disponibili di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione nel computer locale sono incluse nella casella di riepilogo.<br /><br /> Per specificare un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diverso (in esecuzione in modalità tabulare), digitare il nome del server. L'utente connesso deve essere un amministratore nel server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .<br /><br /> Si noti che si consiglia di specificare una variabile locale [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] server come server di area di lavoro. Per database dell'area di lavoro in un server remoto, l'importazione da PowerPivot non è supportata, non è possibile eseguire il backup dei dati in locale e nell'interfaccia utente si potrebbe rilevare latenza durante le query.<br /><br /> Si noti inoltre che l'impostazione predefinita per questa proprietà può essere modificato nella pagina modellazione dati [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] impostazioni in strumenti\finestra di dialogo.|  
  
##  <a name="bkmk_use_ssms"></a> Utilizzo di SSMS per gestire il database dell'area di lavoro  
 È possibile utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) per connettersi al server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui è ospitato il database dell'area di lavoro. In genere non è necessaria alcuna attività di gestione del database dell'area di lavoro. L'unica eccezione è data dallo scollegamento o dall'eliminazione di un database dell'area di lavoro che deve essere eseguita da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!WARNING]  
>  Non usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per gestire il database dell'area di lavoro mentre il progetto è aperto in Progettazione modelli, in quanto si potrebbe verificare una perdita di dati.  
  
##  <a name="bkmk_related_tasks"></a> Attività correlate  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Proprietà modello &#40;SSAS tabulare&#41;](model-properties-ssas-tabular.md)|Fornisce le descrizioni e i passaggi di configurazione per area di lavoro del modello le proprietà del database.|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare la modellazione dei dati e le proprietà di distribuzione predefinite &#40;SSAS tabulare&#41;](configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Proprietà del progetto &#40;SSAS tabulare&#41;](properties-ssas-tabular.md)  
  
  
