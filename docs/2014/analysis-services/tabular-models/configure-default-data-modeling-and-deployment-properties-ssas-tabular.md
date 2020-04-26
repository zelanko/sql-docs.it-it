---
title: Configurare la modellazione dei dati e le proprietà di distribuzione predefinite (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.deployment.f1
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DATA_MODELING
- sql12.asvs.bidtoolset.asoptions.f1
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DEPLOYMENT
ms.assetid: 140d0c4e-943c-4387-a8d2-6e066c7e4e75
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1246119b72890bc80125034c8ee23bcd0c221b5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "66067586"
---
# <a name="configure-default-data-modeling-and-deployment-properties-ssas-tabular"></a>Configurare la modellazione dei dati e le proprietà di distribuzione predefinite (SSAS tabulare)
  Questo argomento descrive come configurare le impostazioni delle proprietà del livello di compatibilità, della distribuzione e del database dell'area di lavoro predefiniti, che possono essere predefinite per ogni nuovo progetto di modello tabulare creato in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Dopo aver creato un nuovo progetto, queste proprietà possono comunque essere modificate in base a requisiti specifici.  
  
#### <a name="to-configure-the-default-compatibility-level-property-setting-for-new-model-projects"></a>Per configurare l'impostazione della proprietà del livello di compatibilità predefinito per nuovi progetti di modello  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic sul menu **Strumenti** , quindi su **Opzioni**.  
  
2.  Nella finestra di dialogo **Opzioni** espandere **Analysis Services Tabular Designers**, quindi fare clic su **Livello di compatibilità**.  
  
3.  Configurare le seguenti impostazioni delle proprietà:  
  
    |Proprietà|Impostazione predefinita|Descrizione|  
    |--------------|---------------------|-----------------|  
    |**Livello di compatibilità predefinito per nuovi progetti**|SQL Server 2012 (1100)|Questa impostazione consente di specificare il livello di compatibilità predefinito da utilizzare per la creazione di un nuovo progetto di modello tabulare. È possibile scegliere SQL Server 2012 RTM (1100) se la distribuzione verrà eseguita in un'istanza di Analysis Services senza SP1 applicato, SQL Server 2012 SP1 se per l'istanza di distribuzione è applicato SP1 oppure SQL Server 2014. Per ulteriori informazioni, vedere [livello di compatibilità &#40;SSAS tabulare SP1&#41;](compatibility-level-for-tabular-models-in-analysis-services.md).|  
    |**Opzioni del livello di compatibilità**|Tutte selezionate|Specifica le opzioni del livello di compatibilità per i nuovi progetti di modello tabulare e in caso di distribuzione in un'altra istanza di Analysis Services.|  
  
#### <a name="to-configure-the-default-deployment-server-property-setting-for-new-model-projects"></a>Per configurare l'impostazione della proprietà del server di distribuzione predefinito per nuovi progetti di modello  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic sul menu **Strumenti** , quindi su **Opzioni**.  
  
2.  Nella finestra di dialogo **Opzioni** espandere **Analysis Services Tabular Designers**, quindi fare clic su **Distribuzione**.  
  
3.  Configurare le seguenti impostazioni delle proprietà:  
  
    |Proprietà|Impostazione predefinita|Descrizione|  
    |--------------|---------------------|-----------------|  
    |**Server di distribuzione predefinito**|localhost|Questa impostazione consente di specificare il server predefinito da utilizzare in caso di distribuzione di un modello. È possibile fare clic sulla freccia GIÙ per cercare i server Analysis Services della rete locale utilizzabili; in alternativa, è possibile digitare il nome di un server remoto.|  
  
    > [!NOTE]  
    >  Le modifiche apportate all'impostazione delle proprietà Server di distribuzione predefinito non influiranno sui progetti esistenti creati prima delle modifiche.  
  
###  <a name="to-configure-the-default-workspace-database-property-settings-for-new-model-projects"></a><a name="bkmk_conf_default"></a> Per configurare l'impostazione della proprietà del database dell'area di lavoro predefinito per nuovi progetti di modello  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic sul menu **Strumenti** , quindi su **Opzioni**.  
  
2.  Nella finestra di dialogo **Opzioni** espandere **Analysis Services Tabular Designers**, quindi fare clic su **Database dell'area di lavoro**.  
  
3.  Configurare le seguenti impostazioni delle proprietà:  
  
    |Proprietà|Impostazione predefinita|Descrizione|  
    |--------------|---------------------|-----------------|  
    |**Server dell'area di lavoro predefinito**|**localhost**|Questa proprietà consente di specificare il server predefinito che sarà utilizzato per ospitare il database dell'area di lavoro mentre si crea il modello in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Tutte le istanze disponibili di Analysis Services in esecuzione sul computer locale sono incluse nella casella di riepilogo.<br /><br /> Nota: si consiglia di specificare sempre un server Analysis Services locale come server dell'area di lavoro. Per database dell'area di lavoro su un server remoto, l'importazione di dati da PowerPivot non è supportata, non è possibile eseguire il backup dei dati in locale e nell'interfaccia utente si potrebbe rilevare latenza durante le query.|  
    |**Memorizzazione del database dell'area di lavoro dopo la chiusura del modello**|**Mantieni i database dell'area di lavoro su disco ma scarica dalla memoria**|Viene specificato come viene mantenuto un database dell'area di lavoro dopo la chiusura di un modello. In un database dell'area di lavoro sono inclusi i metadati del modello, i dati importati in un modello e le credenziali di rappresentazione (crittografate). In alcuni casi, le dimensioni del database dell'area di lavoro possono essere elevate e occupare quindi una quantità notevole di memoria. Per impostazione predefinita, i database dell'area di lavoro vengono rimossi dalla memoria. Quando si modifica questa impostazione, è importante considerare le risorse di memoria disponibili nonché pianificare la frequenza con la quale utilizzare il modello. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> **Mantieni aree di lavoro in memoria** : viene specificato di mantenere le aree di lavoro in memoria dopo la chiusura di un modello. Per questa opzione verrà utilizzata più memoria; tuttavia, in caso di apertura di un modello in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vengono utilizzate meno risorse e i carichi nell'area di lavoro verranno eseguiti più velocemente.<br /><br /> **Mantieni i database dell'area di lavoro su disco ma scarica dalla memoria** : viene specificato di mantenere il database dell'area di lavoro su disco, ma non più in memoria dopo la chiusura di un modello. Per questa opzione verrà utilizzata meno memoria; tuttavia, in caso di apertura di un modello in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vengono utilizzate risorse aggiuntive e il caricamento del modello sarà più lento rispetto a quando il database dell'area di lavoro è mantenuto in memoria. Utilizzare questa opzione quando le risorse in memoria sono limitate o quando in uso in un database dell'area di lavoro remoto.<br /><br /> **Elimina area di lavoro** : viene specificato di eliminare il database dell'area di lavoro dalla memoria e di non mantenerlo su disco dopo la chiusura del modello. Per questa opzione verranno usati meno memoria e meno spazio di archiviazione; tuttavia, in caso di apertura di un modello in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vengono usate risorse aggiuntive e il caricamento del modello sarà più lento rispetto a quando il database dell'area di lavoro è mantenuto in memoria o su disco. Utilizzare questa opzione quando i modelli vengono utilizzati solo occasionalmente.|  
    |**Backup dei dati**|**Mantieni il backup dei dati su disco**|Viene specificato se viene mantenuto o meno un backup dei dati del modello in un file di backup. Per questa impostazione della proprietà sono disponibili le opzioni seguenti:<br /><br /> **Mantieni il backup dei dati su disco** : viene specificato di mantenere un backup dei dati del modello su disco. Quando il modello viene salvato, anche i dati vengono salvati nel file (ABF) di backup. La selezione di questa opzione può comportare tempi di caricamento e salvataggio del modello più lenti.<br /><br /> **Non mantenere il backup dei dati su disco** : viene specificato di non mantenere un backup dei dati del modello su disco. Questa opzione consentirà di ridurre i tempi di salvataggio e caricamento del modello.|  
  
> [!NOTE]  
>  Le modifiche apportate alle proprietà del modello predefinito non influiranno sulle proprietà dei modelli esistenti creati prima delle modifiche.  
  
## <a name="see-also"></a>Vedi anche  
 [Proprietà del progetto &#40;SSAS tabulare&#41;](properties-ssas-tabular.md)   
 [Proprietà del modello &#40;SSAS tabulare&#41;](model-properties-ssas-tabular.md)   
 [Livello di compatibilità &#40;SSAS tabulare SP1&#41;](compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
