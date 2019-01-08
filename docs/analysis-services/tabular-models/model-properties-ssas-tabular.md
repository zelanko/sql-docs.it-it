---
title: Proprietà del modello tabulare di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d9251a09039d93d473963ced235669c66f99431b
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072188"
---
# <a name="model-properties"></a>Proprietà dei modelli 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Questo articolo descrive le proprietà del modello tabulare. Ogni progetto di modello tabulare ha proprietà del modello che influiscono su come viene eseguito il backup e su come viene compilato il modello durante la creazione in Strumenti di sviluppo di SQL Server, nonché su come viene archiviato il database dell'area di lavoro. Le proprietà del modello descritte in questo argomento non vengono applicate ai modelli che sono già stati distribuiti.  
  
 Sezioni dell'argomento:  
  
-   [Proprietà dei modelli](#bkmk_model_properties)  
  
-   [Configurare le impostazioni delle proprietà dei modelli](#bkmk_conf_model_prop)  
  
##  <a name="bkmk_model_properties"></a> Proprietà del modello  
 **Advanced**  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Azione di compilazione**|Compila|Questa proprietà consente di specificare la modalità di correlazione del file al processo di compilazione e distribuzione. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> **Compilare** -si verifica una normale azione di compilazione. Le definizioni per gli oggetti modello verranno scritte nel file con estensione asdatabase.<br /><br /> **Nessuno** -l'output del file con estensione asdatabase sarà vuoto.|  
|**Copia nella directory di output**|Non copiare|Questa proprietà consente di specificare il file di origine che sarà copiato nella directory di output. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> **Non copiare** -viene creata alcuna copia nella directory di output.<br /><br /> **Copia sempre** -viene sempre creata una copia nella directory di output.<br /><br /> **Copia se più recente** : viene creata una copia nella directory di output solo se sono state apportate modifiche al file model.bim.|  
  
 **Varie**  
  
> [!NOTE]  
>  Alcune proprietà vengono impostate automaticamente quando si crea il modello e non possono essere modificate.  
  
> [!NOTE]  
>  Le proprietà Server dell'area di lavoro, Memorizzazione area di lavoro e Backup dei dati dispongono di impostazioni predefinite applicate quando si crea un nuovo progetto di modello. È possibile modificare le impostazioni predefinite per nuovi modelli nella pagina Modellazione dati nelle impostazioni di Analysis Server in Strumenti\finestra di dialogo Opzioni. Queste proprietà, come altre, possono essere impostate anche per ogni modello nella finestra Proprietà. Per altre informazioni, vedere [configurare le proprietà di modellazione e alla distribuzione dei dati predefinite](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Regole di confronto**|Regole di confronto predefinite per il computer per il quale viene installato Visual Studio.|Designazione regole di confronto per il modello.|  
|**Livello di compatibilità**|Valore predefinito o di altro tipo selezionato in fase di creazione del progetto.|Si applica a SQL Server 2012 Analysis Services SP1 o versione successiva. Specifica le funzionalità e le impostazioni disponibili per il modello. Per informazioni dettagliate, vedere [Livello di compatibilità per i modelli tabulari in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).|  
|**Backup dei dati**|Non eseguire il backup su disco|Viene specificato se viene mantenuto o meno un backup dei dati del modello in un file di backup. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> **Esegui il backup su disco** : viene specificato di mantenere un backup dei dati del modello su disco. Quando il modello viene salvato, anche i dati vengono salvati nel file (ABF) di backup. La selezione di questa opzione può comportare tempi di caricamento e salvataggio del modello più lenti.<br /><br /> **Non eseguire il backup su disco** : viene specificato di non mantenere un backup dei dati del modello su disco. Questa opzione consentirà di ridurre i tempi di salvataggio e caricamento del modello.<br /><br /> <br /><br /> L'impostazione predefinita per questa proprietà può essere modificata nella pagina Modellazione dati nelle impostazioni di Analysis Server in Strumenti\finestra di dialogo Opzioni.| 
|**Direzione filtro predefinita**|Per direzione singola|Determina la direzione del filtro predefinito per nuove relazioni.| 
|**Modalità DirectQuery**|Disattivato|Viene specificato se questo modello funziona nella modalità DirectQuery. Per altre informazioni, vedere [la modalità DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).|  
|**Nome file**|Model.bim|Viene specificato il nome del file con estensione bim. È consigliabile non modificare il nome del file.|  
|**Percorso completo**|Percorso specificato durante la creazione del progetto.|Percorso del file model.bim. Questa proprietà non può essere impostata nella finestra Proprietà.|  
|**Lingua**|Inglese|Lingua predefinita del modello. La lingua predefinita è determinata dalla lingua di Visual Studio. Questa proprietà non può essere impostata nella finestra Proprietà.|  
|**Database dell'area di lavoro**|Nome del progetto, seguito da una carattere di sottolineatura e da un GUID.|Nome del database dell'area di lavoro utilizzato per l'archiviazione e la modifica del modello in memoria per il file model.bim selezionato. Questo database verrà visualizzato nell'istanza di Analysis Services specificata nella proprietà Workspace Server. Questa proprietà non può essere impostata nella finestra Proprietà. Per altre informazioni, vedere [dell'area di lavoro Database](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md).|  
|**Memorizzazione area di lavoro**|Scarica dalla memoria|Viene specificato come viene mantenuto un database dell'area di lavoro dopo la chiusura di un modello. In un database dell'area di lavoro sono inclusi i metadati del modello, i dati importati in un modello e le credenziali di rappresentazione (crittografate). In alcuni casi, le dimensioni del database dell'area di lavoro possono essere elevate e occupare quindi una quantità notevole di memoria. Per impostazione predefinita, i database dell'area di lavoro vengono scaricati dalla memoria. Quando si modifica questa impostazione, è importante considerare le risorse di memoria disponibili nonché pianificare la frequenza con la quale utilizzare il modello. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> **Mantieni in memoria** : viene specificato di mantenere il database dell'area di lavoro in memoria dopo la chiusura di un modello. Questa opzione utilizza una maggior quantità di memoria, tuttavia, quando si apre un modello, vengono utilizzate meno risorse e il database dell'area di lavoro viene caricato più velocemente.<br /><br /> **Scarica dalla memoria** : viene specificato di mantenere il database dell'area di lavoro su disco, ma non più in memoria dopo la chiusura di un modello. Questa opzione utilizza una minor quantità di memoria, tuttavia, quando si apre un modello, vengono utilizzate ulteriori risorse e il caricamento del modello risulta più lento rispetto a quando il database dell'area di lavoro viene mantenuto in memoria. Utilizzare questa opzione quando le risorse in memoria sono limitate o quando in uso in un database dell'area di lavoro remoto.<br /><br /> **Elimina area di lavoro** : viene specificato di eliminare il database dell'area di lavoro dalla memoria e di non mantenerlo su disco dopo la chiusura del modello. Questa opzione utilizza una minor quantità di memoria e di spazio di archiviazione, tuttavia, quando si apre un modello, vengono utilizzate ulteriori risorse e il caricamento del modello risulta più lento rispetto a quando il database dell'area di lavoro viene mantenuto in memoria o su disco. Utilizzare questa opzione quando i modelli vengono utilizzati solo occasionalmente.<br /><br /> <br /><br /> L'impostazione predefinita per questa proprietà può essere modificata nella pagina Modellazione dati nelle impostazioni di Analysis Server in Strumenti\finestra di dialogo Opzioni.|  
|**Server dell'area di lavoro**|localhost|Questa proprietà specifica il server predefinito usato per ospitare il database dell'area di lavoro mentre si crea il modello. Tutte le istanze disponibili di Analysis Services in esecuzione sul computer locale sono incluse nella casella di riepilogo.<br /><br /> L'impostazione predefinita per questa proprietà può essere modificata nella pagina Modellazione dati nelle impostazioni di Analysis Server in Strumenti\finestra di dialogo Opzioni.<br /><br /> <br /><br /> Nota: Si consiglia di specificare sempre un server Analysis Services locale come server dell'area di lavoro. Per i database dell'area di lavoro in un server remoto, l'importazione da [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] non è supportata, il backup dei dati non può essere eseguito in locale e l'interfaccia utente può essere soggetta a latenza durante le query.|  
  
##  <a name="bkmk_conf_model_prop"></a> Configurare le impostazioni delle proprietà dei modelli  
  
1.  In **Esplora soluzioni**di SSDT fare clic sul file **Model.bim** .  
  
2.  Nella finestra **Proprietà** fare clic su una proprietà, quindi digitare un valore o fare clic sulla freccia GIÙ per selezionare un'opzione di impostazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le proprietà di modellazione e alla distribuzione dei dati predefinite](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Proprietà progetto](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
