---
title: Proprietà del modello (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.fileprop.f1
- sql12.asvs.bidtoolset.wspacedbconfig.f1
ms.assetid: 8ab04656-75a5-485c-9687-7b1ca49f7f80
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 47ca12ee0118e0c2b63da05cf2d508ec0c2f5f92
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66066959"
---
# <a name="model-properties-ssas-tabular"></a>Proprietà modello (SSAS tabulare)
  In questo argomento vengono descritte le proprietà dei modelli tabulari. Ogni progetto di modello tabulare in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] dispone di proprietà del modello che influiscono sulle modalità di compilazione del modello in fase di creazione, di esecuzione del backup, nonché di archiviazione del database dell'area di lavoro. Le proprietà del modello descritte in questo argomento non vengono applicate ai modelli che sono già stati distribuiti.  
  
 Sezioni dell'argomento:  
  
-   [Proprietà dei modelli](#bkmk_model_properties)  
  
-   [Per configurare le impostazioni delle proprietà dei modelli](#bkmk_conf)  
  
##  <a name="model-properties"></a><a name="bkmk_model_properties"></a>Proprietà modello  
 **Avanzate**  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Azione di compilazione**|Compilazione|Questa proprietà consente di specificare la modalità di correlazione del file al processo di compilazione e distribuzione. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> **Compilazione** : viene eseguita una normale azione di compilazione. Le definizioni per gli oggetti modello verranno scritte nel file con estensione asdatabase.<br /><br /> **Nessuno** : l'output del file con estensione asdatabase sarà vuoto.|  
|**Copia nella directory di output**|Non copiare|Questa proprietà consente di specificare il file di origine che sarà copiato nella directory di output. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> Non **copiare** : non viene creata alcuna copia nella directory di output.<br /><br /> **Copy always** : viene sempre creata una copia nella directory di output.<br /><br /> **Copia se più recente** : viene creata una copia nella directory di output solo se sono state apportate modifiche al file model.bim.|  
  
 **Varie**  
  
> [!NOTE]  
>  Alcune proprietà vengono impostate automaticamente quando si crea il modello e non possono essere modificate.  
  
> [!NOTE]  
>  Le proprietà Server dell'area di lavoro, Memorizzazione area di lavoro e Backup dei dati dispongono di impostazioni predefinite applicate quando si crea un nuovo progetto di modello. È possibile modificare le impostazioni predefinite per nuovi modelli nella pagina Modellazione dati nelle impostazioni di Analysis Server in Strumenti\finestra di dialogo Opzioni. Queste proprietà, come altre, possono essere impostate anche per ogni modello nella finestra Proprietà. Per altre informazioni, vedere [Configurare la modellazione dei dati e le proprietà di distribuzione predefinite &#40;SSAS tabulare&#41;](properties-ssas-tabular.md).  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Regole di confronto**|Regole di confronto predefinite per il computer per il quale viene installato Visual Studio.|Designazione regole di confronto per il modello.|  
|**Livello di compatibilità**|Valore predefinito o di altro tipo selezionato in fase di creazione del progetto.|Si applica a SQL Server 2012 Analysis Services SP1 o versione successiva. Specifica le funzionalità e le impostazioni disponibili per il modello. Per ulteriori informazioni, vedere [livello di compatibilità &#40;SSAS tabulare SP1&#41;](compatibility-level-for-tabular-models-in-analysis-services.md).|  
|**Backup dei dati**|Non eseguire il backup su disco|Viene specificato se viene mantenuto o meno un backup dei dati del modello in un file di backup. Si noti che l'impostazione predefinita per questa proprietà può essere modificata nella pagina modellazione dati in Analysis Server impostazioni della finestra di dialogo Strumenti\finestra. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> **Esegui il backup su disco** : viene specificato di mantenere un backup dei dati del modello su disco. Quando il modello viene salvato, anche i dati vengono salvati nel file (ABF) di backup. La selezione di questa opzione può comportare tempi di caricamento e salvataggio del modello più lenti.<br /><br /> **Non eseguire il backup su disco** : viene specificato di non mantenere un backup dei dati del modello su disco. Questa opzione consentirà di ridurre i tempi di salvataggio e caricamento del modello.|  
|**Modalità DirectQuery**|Disattivato|Viene specificato se questo modello funziona nella modalità DirectQuery. Per altre informazioni, vedere [Modalità DirectQuery &#40;SSAS tabulare&#41;](directquery-mode-ssas-tabular.md).|  
|**Nome file**|Model.bim|Viene specificato il nome del file con estensione bim. È consigliabile non modificare il nome del file.|  
|**Percorso completo**|Percorso specificato durante la creazione del progetto.|Percorso del file model.bim. Questa proprietà non può essere impostata nella finestra Proprietà.|  
|**Lingua**|Inglese|Lingua predefinita del modello. La lingua predefinita è determinata dalla lingua di Visual Studio. Questa proprietà non può essere impostata nella finestra Proprietà.|  
|**Database dell'area di lavoro**|Nome del progetto, seguito da una carattere di sottolineatura e da un GUID.|Nome del database dell'area di lavoro utilizzato per l'archiviazione e la modifica del modello in memoria per il file model.bim selezionato. Questo database verrà visualizzato nell'istanza di Analysis Services specificata nella proprietà Workspace Server. Questa proprietà non può essere impostata nella finestra Proprietà. Per altre informazioni, vedere [Database dell'area di lavoro &#40;SSAS tabulare&#41;](workspace-database-ssas-tabular.md).|  
|**Memorizzazione area di lavoro**|Scarica dalla memoria|Viene specificato come viene mantenuto un database dell'area di lavoro dopo la chiusura di un modello. In un database dell'area di lavoro sono inclusi i metadati del modello, i dati importati in un modello e le credenziali di rappresentazione (crittografate). In alcuni casi, le dimensioni del database dell'area di lavoro possono essere elevate e occupare quindi una quantità notevole di memoria. Per impostazione predefinita, i database dell'area di lavoro vengono scaricati dalla memoria. Quando si modifica questa impostazione, è importante considerare le risorse di memoria disponibili nonché pianificare la frequenza con la quale utilizzare il modello. Si noti che l'impostazione predefinita per questa proprietà può essere modificata nella pagina modellazione dati in Analysis Server impostazioni della finestra di dialogo Strumenti\finestra. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> **Mantieni in memoria** : viene specificato di mantenere il database dell'area di lavoro in memoria dopo la chiusura di un modello. Per questa opzione verrà utilizzata più memoria; tuttavia, in caso di apertura di un modello in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vengono utilizzate meno risorse e i carichi nel database dell'area di lavoro verranno eseguiti più velocemente.<br /><br /> **Scarica dalla memoria** : viene specificato di mantenere il database dell'area di lavoro su disco, ma non più in memoria dopo la chiusura di un modello. Per questa opzione verrà utilizzata meno memoria; tuttavia, in caso di apertura di un modello in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vengono utilizzate risorse aggiuntive e il caricamento del modello sarà più lento rispetto a quando il database dell'area di lavoro è mantenuto in memoria. Utilizzare questa opzione quando le risorse in memoria sono limitate o quando in uso in un database dell'area di lavoro remoto.<br /><br /> **Elimina area di lavoro** : viene specificato di eliminare il database dell'area di lavoro dalla memoria e di non mantenerlo su disco dopo la chiusura del modello. Per questa opzione verranno usati meno memoria e meno spazio di archiviazione; tuttavia, in caso di apertura di un modello in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vengono usate risorse aggiuntive e il caricamento del modello sarà più lento rispetto a quando il database dell'area di lavoro è mantenuto in memoria o su disco. Utilizzare questa opzione quando i modelli vengono utilizzati solo occasionalmente.|  
|**Server dell'area di lavoro**|localhost|Questa proprietà consente di specificare il server predefinito che sarà utilizzato per ospitare il database dell'area di lavoro mentre si crea il modello in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Tutte le istanze disponibili di Analysis Services in esecuzione sul computer locale sono incluse nella casella di riepilogo.<br /><br /> Nota: si consiglia di specificare sempre un server Analysis Services locale come server dell'area di lavoro. Per database dell'area di lavoro su un server remoto, l'importazione da PowerPivot non è supportata, non è possibile eseguire il backup dei dati in locale e nell'interfaccia utente si potrebbe rilevare latenza durante le query.<br /><br /> L'impostazione predefinita per questa proprietà può essere modificata nella pagina Modellazione dati nelle impostazioni di Analysis Server in Strumenti\finestra di dialogo Opzioni.|  
  
##  <a name="bkmk_conf_model_prop"></a>   
###  <a name="to-configure-model-property-settings"></a><a name="bkmk_conf"></a>Per configurare le impostazioni delle proprietà del modello  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]in **Esplora soluzioni**fare clic sul file **Model.bim** .  
  
2.  Nella finestra **Proprietà** fare clic su una proprietà, quindi digitare un valore o fare clic sulla freccia GIÙ per selezionare un'opzione di impostazione.  
  
## <a name="see-also"></a>Vedi anche  
 [Configurare la modellazione dei dati e le proprietà di distribuzione predefinite &#40;SSAS tabulare&#41;](properties-ssas-tabular.md)   
 [Proprietà del progetto &#40;SSAS tabulare&#41;](project-properties-ssas-tabular.md)  
  
  
