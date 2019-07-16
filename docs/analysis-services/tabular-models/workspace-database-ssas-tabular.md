---
title: Il database dell'area di lavoro di Analysis Services in SQL Server Data Tools | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b3f9d94d35d5aaa4ea86cf1f1d9dc845b67eaf4f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162344"
---
# <a name="workspace-database"></a>Database dell'area di lavoro

[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Il database dell'area di lavoro modello tabulare, usato durante la creazione del modello, viene creato quando si crea un nuovo progetto di modello tabulare in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].
  
## <a name="specifying-a-workspace-instance"></a>Specifica di un'istanza dell'area di lavoro  

  Quando si crea un nuovo progetto di modello tabulare in SSDT, è possibile specificare un'istanza di Analysis Services da usare durante la creazione del progetto. A partire dal rilascio di settembre 2016 (14.0.60918.0) di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], sono disponibili due modalità per specificare un'istanza dell'area di lavoro quando si crea un nuovo progetto di modello tabulare. 

**Area di lavoro integrata** - scelta consigliata. Usa l'istanza di Analysis Services interna di SSDT. Usare questa impostazione quando si crea un progetto che verrà distribuita in Azure Analysis Services.

**Server dell'area di lavoro** : viene creato un database dell'area di lavoro in un'istanza di Analysis Services esplicita, spesso nello stesso computer di SSDT o in un altro computer della stessa rete. Anche se è possibile specificare un server Azure Analysis Services, non è consigliabile. 
  
### <a name="integrated-workspace"></a>Area di lavoro integrata

Con l'Area di lavoro integrata viene creato un database di lavoro in memoria usando un'istanza di Analysis Services implicita di SSDT. Modalità area di lavoro integrata riduce notevolmente la complessità della creazione di progetti tabulari in SSDT perché non è richiesto un server Analysis Services esplicito separato.

Usando la modalità Area di lavoro integrata, SSDT tabulare avvia dinamicamente l'istanza interna di SSAS in background e carica il database. È possibile aggiungere e visualizzare tabelle, colonne e dati in Progettazione modelli. Se si aggiungono altre tabelle, colonne, relazioni e così via, viene modificato il database dell'area di lavoro. La modalità Area di lavoro integrata non modifica il modo in cui SSDT tabulare gestisce un server e un database dell'area di lavoro. Ciò che cambia è la posizione in cui SSDT tabulare ospita il database dell'area di lavoro.

È possibile selezionare la modalità Area di lavoro integrata quando si crea un nuovo modello di progetto tabulare in SSDT.

![Modalità area di lavoro integrata in SSAS](../../analysis-services/tabular-models/media/ssas-integrated-workspace-mode.png)

Usando le proprietà Database dell'area di lavoro e Server dell'area di lavoro per model.bim, è possibile individuare il nome del database temporaneo e la porta TCP dell'istanza interna di SSAS in cui SSDT tabulare ospita il database. È possibile connettersi al database dell'area di lavoro con SSMS, purché in SSDT tabulare sia caricato il database. L'impostazione Memorizzazione area di lavoro specifica che SSDT tabulare mantiene il database dell'area di lavoro su disco, ma non più in memoria dopo la chiusura di un progetto di modello. In questo modo verrà utilizzata meno memoria rispetto a quella che verrebbe utilizzata se il modello fosse mantenuto sempre in memoria. Se si vogliono controllare queste impostazioni, impostare la proprietà Modalità area di lavoro integrata su False e quindi specificare un server dell'area di lavoro esplicito. Un server dell'area di lavoro esplicito anche rendere anzi se i dati da importare in un modello superano la capacità di memoria della workstation di SSDT.

> [!NOTE]  
>  Quando si usa la modalità area di lavoro integrata, l'istanza di Analysis Services locale è a 64 bit, mentre SSDT è in esecuzione nell'ambiente a 32 bit di Visual Studio. Se ci si connette a origini dati speciali, assicurarsi di installare entrambe le versioni a 32 bit e 64 bit dei provider di dati corrispondenti nella workstation. Il provider a 64 bit è necessario per l'istanza di Analysis Services a 64 bit e la versione a 32 bit è necessaria per l'importazione guidata tabella in SSDT.

###  <a name="bkmk_overview"></a> Server dell'area di lavoro


 Un database dell'area di lavoro viene creato nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , specificata nella proprietà Server dell'area di lavoro, quando si crea un nuovo progetto di business intelligence tramite uno dei modelli del progetto di modello tabulare in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Ogni progetto di modello tabulare disporrà del relativo database dell'area di lavoro. È possibile utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per visualizzare il database dell'area di lavoro nel server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Nel nome del database dell'area di lavoro è incluso il nome del progetto, seguito da un carattere di sottolineatura, dal nome utente, da un carattere di sottolineatura e infine da un GUID.  
  
 Il database dell'area di lavoro si trova in memoria mentre il progetto di modello tabulare viene aperto in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Quando si chiude il progetto, il database dell'area di lavoro può essere mantenuto in memoria, archiviato su disco e rimosso dalla memoria (impostazione predefinita) o essere rimosso dalla memoria e non archiviato su disco, come determinato dalla proprietà Memorizzazione area di lavoro. Per altre informazioni sulla proprietà Memorizzazione area di lavoro, vedere le [proprietà del database dell'area di lavoro](#bkmk_ws_prop) più avanti in questo argomento.  
  
 Dopo avere aggiunto dati al progetto di modello tramite l'Importazione guidata tabella o un'operazione di copia e incolla, quando si visualizzano le tabelle, le colonne e i dati in Progettazione modelli, viene in pratica visualizzato il database dell'area di lavoro. Se si aggiungono altre tabelle, colonne, relazioni e così via, il database dell'area di lavoro viene modificato.  
  
 Quando si distribuisce un progetto di modello tabulare, il database del modello distribuito, che essenzialmente è una copia del database dell'area di lavoro, viene creato nell'istanza del server Analysis Services specificata nella proprietà Server di distribuzione. Per altre informazioni sulla proprietà del Server di distribuzione, vedere [proprietà del progetto](../../analysis-services/tabular-models/project-properties-ssas-tabular.md).  
  
 Il database dell'area di lavoro modello si trova in genere nel localhost o in un'istanza denominata locale di un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . È possibile utilizzare un'istanza remota di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per ospitare il database dell'area di lavoro, ma si tratta di una configurazione non consigliata a causa della latenza durante le query dei dati e di altre restrizioni. In modo ottimale, l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui verranno ospitati i database dell'area di lavoro si trova nello stesso computer di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. La creazione di progetti di modello nello stesso computer dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui è ospitato il database dell'area di lavoro può migliorare le prestazioni.  
  
 I database dell'area di lavoro remoti presentano le restrizioni seguenti:  
  
-   Possibile latenza durante le query.  
  
-   Non è possibile impostare la proprietà Backup dei dati sull'opzione relativa al **backup su disco**.  
  
-   Non è possibile importare dati da una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] quando si crea un nuovo progetto di modello tabulare usando il modello di progetto per l'importazione da [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
  > [!IMPORTANT]  
>  Il livello di compatibilità del modello e il server dell'area di lavoro devono corrispondere.
  
> [!NOTE]  
>  Se una tabella nel modello conterrà un numero considerevole di righe, si consideri di importare solo un subset dei dati durante la creazione di modelli. L'importazione di un subset dei dati consente di ridurre tempi di elaborazione e utilizzo delle risorse server per il database dell'area di lavoro.  
  
> [!NOTE]  
>  Nella finestra di anteprima delle finestre di dialogo Modifica proprietà tabella e Gestione partizioni della pagina Selezione tabelle e viste nell'Importazione guidata tabella vengono visualizzate tabelle, colonne e righe nell'origine dati e potrebbero non essere mostrate le stesse tabelle, colonne e righe del database dell'area di lavoro.  
  
  
##  <a name="bkmk_ws_prop"></a> proprietà del database dell'area di lavoro  
 Le proprietà del database dell'area di lavoro sono incluse nelle proprietà del modello. Per visualizzare le proprietà dei modelli, in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]Esplora soluzioni **di**fare clic sul file **Model.bim** . Le proprietà dei modelli possono essere configurate usando la finestra **Proprietà** . Nelle proprietà specifiche del database dell'area di lavoro è incluso quanto indicato di seguito:  
  
> [!NOTE]  
>  Le proprietà **Modalità area di lavoro integrata**, **Server dell'area di lavoro**, **Memorizzazione area di lavoro** e **Backup dei dati** hanno impostazioni predefinite che vengono applicate quando si crea un nuovo progetto di modello. È possibile modificare le impostazioni predefinite per nuovi progetti di modello nella pagina **Modellazione dati** nelle impostazioni di **Analysis Server** in Strumenti\finestra di dialogo Opzioni. Queste proprietà, come altre, possono essere impostate anche per ogni progetto di modello nella finestra **Proprietà** . Le modifiche apportate alle impostazioni predefinite non verranno applicate ai progetti di modello già creati. Per altre informazioni, vedere [configurare le proprietà di modellazione e alla distribuzione dei dati predefinite](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Modalità area di lavoro integrata**|True, False|Se si seleziona la modalità Area di lavoro integrata per il database dell'area di lavoro quando viene creato il progetto, questa proprietà sarà True. Se si seleziona la modalità **Server dell'area di lavoro** quando viene creato il progetto, questa proprietà sarà False. | 
|**Database dell'area di lavoro**|Nome|Nome del database dell'area di lavoro. Questa proprietà non può essere modificata se **Modalità area di lavoro integrata** è **True**.|  
|**Memorizzazione area di lavoro**|Scarica dalla memoria|Viene specificato come viene mantenuto un database dell'area di lavoro dopo la chiusura di un progetto di modello. In un database dell'area di lavoro sono inclusi i metadati del modello e i dati importati. In alcuni casi, le dimensioni del database dell'area di lavoro possono essere elevate e utilizzare quindi una grande quantità di memoria. Per impostazione predefinita, quando si chiude un progetto di modello in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], il database dell'area di lavoro viene scaricato dalla memoria. Quando si modifica questa impostazione, è importante considerare le risorse di memoria disponibili, nonché pianificare la frequenza con la quale utilizzare il progetto di modello. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> **Mantieni in memoria** : viene specificato di mantenere il database dell'area di lavoro in memoria dopo la chiusura di un progetto di modello. Per questa opzione verrà utilizzata più memoria; tuttavia, in caso di apertura di un progetto di modello in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], vengono utilizzate meno risorse e i carichi nel database dell'area di lavoro verranno eseguiti più velocemente.<br /><br /> **Scarica dalla memoria** : viene specificato di mantenere il database dell'area di lavoro su disco, ma non più in memoria dopo la chiusura di un progetto di modello. Per questa opzione verrà usa meno memoria. Tuttavia, in caso di apertura di un progetto di modello in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], il database dell'area di lavoro deve essere collegato di nuovo. Vengono usate risorse aggiuntive e il caricamento del progetto di modello sarà più lento rispetto a quando il database dell'area di lavoro è mantenuto in memoria. Utilizzare questa opzione quando le risorse in memoria sono limitate o quando in uso in un database dell'area di lavoro remoto.<br /><br /> **Elimina area di lavoro** : viene specificato di eliminare il database dell'area di lavoro dalla memoria e di non mantenerlo su disco dopo la chiusura del progetto di modello. Per questa opzione verranno usati meno memoria e meno spazio di archiviazione. Tuttavia, in caso di apertura di un progetto di modello in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], vengono use risorse aggiuntive e il caricamento del progetto di modello sarà più lento rispetto a quando il database dell'area di lavoro è mantenuto in memoria o su disco. Utilizzare questa opzione quando i progetti di modello vengono utilizzati solo occasionalmente.<br /><br /> L'impostazione predefinita per questa proprietà può essere modificata nella pagina **Modellazione dati** nelle impostazioni di **Analysis Server** in Strumenti\finestra di dialogo Opzioni. Questa proprietà non può essere modificata se **Modalità area di lavoro integrata** è **True**.|  
|**Workspace Server**|localhost|Questa proprietà consente di specificare il server predefinito che sarà utilizzato per ospitare il database dell'area di lavoro mentre si crea il progetto di modello in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Tutte le istanze disponibili di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione nel computer locale sono incluse nella casella di riepilogo.<br /><br /> Per specificare un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diverso (in esecuzione in modalità tabulare), digitare il nome del server. L'utente connesso deve essere un amministratore nel server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .<br /><br /> Si consiglia di specificare un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] locale come server dell'area di lavoro. Per i database dell'area di lavoro in un server remoto, l'importazione da [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] non è supportata, il backup dei dati non può essere eseguito in locale e l'interfaccia utente può essere soggetta a latenza durante le query.<br /><br /> L'impostazione predefinita per questa proprietà può essere modificata nella pagina Modellazione dati nelle impostazioni di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in Strumenti\finestra di dialogo Opzioni. Questa proprietà non può essere modificata se **Modalità area di lavoro integrata** è **True**.|  
  
##  <a name="bkmk_use_ssms"></a> Utilizzo di SSMS per gestire il database dell'area di lavoro  
 È possibile usare SQL Server Management Studio (SSMS) per connettersi a un server di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che ospita un database dell'area di lavoro. In genere non è necessaria alcuna attività di gestione del database dell'area di lavoro. L'unica eccezione è data dallo scollegamento o dall'eliminazione di un database dell'area di lavoro che deve essere eseguita da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Non usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per gestire il database dell'area di lavoro mentre il progetto è aperto in Progettazione modelli, in quanto si potrebbe verificare una perdita di dati.
   
## <a name="see-also"></a>Vedere anche  
[Proprietà dei modelli](../../analysis-services/tabular-models/model-properties-ssas-tabular.md) 
  
  
