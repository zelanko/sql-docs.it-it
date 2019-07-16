---
title: Le proprietà del progetto del modello tabulare di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b695f847ec7f99366e71e76aefe5aecb99cf5933
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162647"
---
# <a name="project-properties"></a>Proprietà di progetti 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Questo articolo descrive le proprietà del progetto modello. Ogni progetto di modello tabulare dispone di proprietà relative alle opzioni e al server di distribuzione che consentono di specificare come vengono distribuiti il progetto e il modello, ad esempio il server in cui verrà distribuito il modello e il nome del database modello distribuito. Queste impostazioni differiscono dalle proprietà dei modelli che interessano invece il database dell'area di lavoro modello. Le proprietà del progetto descritte in questo argomento si trovano nella finestra di dialogo delle proprietà modali, diversa dalla finestra delle proprietà utilizzata per visualizzare altri tipi di proprietà. Per visualizzare queste proprietà, in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Esplora soluzioni **di**fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Proprietà**.  
  
 Sezioni dell'argomento:  
  
-   [Proprietà progetto](#bkmk_proj_properties)  
  
-   [Configurare le impostazioni delle proprietà Opzioni di distribuzione e Server di distribuzione](#bkmk_conf_proj_settings)  
  
##  <a name="bkmk_proj_properties"></a>Proprietà del progetto  
 **Opzioni di distribuzione**  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Opzione di elaborazione**|**Default**|Per impostazione predefinita, in Analysis Services verrà determinato il tipo di elaborazione necessario quando vengono distribuite le modifiche agli oggetti. Ciò garantisce in genere tempi di distribuzione più rapidi. È inoltre possibile, tuttavia, scegliere di eseguire con ogni distribuzione l'elaborazione completa o nessuna elaborazione.|  
|**Distribuzione transazionale**|**False**|Consente di specificare se la distribuzione del modello sia o meno transazionale. Per impostazione predefinita, la distribuzione di tutti gli oggetti o di quelli modificati non è transazionale con l'elaborazione di tali oggetti distribuiti. La distribuzione può avere esito positivo ed essere persistente anche in caso di esito negativo dell'elaborazione. Questa impostazione può essere modificata in modo da incorporare la distribuzione e l'elaborazione in una singola transazione.|  
|**Modalità query**|**In-Memory**|Consente di specificare l'origine da cui vengono restituiti i risultati della query. Per altre informazioni, vedere [la modalità DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).|  
  
 **Server di distribuzione**  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Server**|**localhost**|Consente di specificare un'istanza di Analysis Services. Per impostazione predefinita, i modelli vengono distribuiti nell'istanza predefinita di Analysis Services nel computer locale. Questa impostazione può essere modificata per specificare un'istanza denominata sul computer locale o qualsiasi istanza su qualsiasi computer remoto per cui si dispone dell'autorizzazione necessaria per creare oggetti di Analysis Services. In genere, si tratta delle autorizzazioni di amministratore.<br /><br /> L'impostazione predefinita per questa proprietà può essere modificata utilizzando la proprietà Server di distribuzione predefinito nella pagina Distribuzione delle impostazioni di Analysis Server in Strumenti\finestra di dialogo Opzioni. Per altre informazioni, vedere [configurare le proprietà di modellazione e alla distribuzione dei dati predefinite](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).|  
|**Edizione**|**Sviluppatore**|Consente di specificare l'edizione del server Analysis Services in cui verrà distribuito il modello. L'edizione del server consente di definire le varie funzionalità che possono essere incorporate nel progetto.|  
|**Database**|**Modello**|Consente di specificare il nome del database di Analysis Services in cui verrà creata un'istanza degli oggetti modello durante la distribuzione. Questo nome verrà specificato in una connessione dati o in un file di connessione dati con estensione rsds. È consigliabile che il nome rifletta il tipo di analisi che verrà eseguito utilizzando il modello, ad esempio AdventureWorksSalesModel.<br /><br /> Per evitare nomi duplicati di modelli distribuiti, è consigliabile modificare l'impostazione della proprietà **Nome database** in modo da riflettere lo scopo del modello. Tale nome sarà quello visualizzato dagli utenti quando si connettono al modello come origine dati.|  
|**Nome cubo**|**Modello**|Consente di specificare il nome del cubo del database come mostrato in una connessione ai dati dello strumento client di creazione report.|  
|**Version**|**13.0**|Versione dell'istanza di Analysis Services in cui verrà distribuito il progetto.|  
  
 **Opzioni di DirectQuery**  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Impostazioni di rappresentazione**|**Default**|Consente di specificare le credenziali utilizzate per connettersi alle origini dati per un modello in esecuzione in modalità DirectQuery. Queste credenziali sono diverse da quelle della rappresentazione utilizzate nella modalità In memoria predefinita. Per altre informazioni, vedere [rappresentazione](../../analysis-services/tabular-models/impersonation-ssas-tabular.md).|  
  
##  <a name="bkmk_conf_proj_settings"></a> Configurare le impostazioni delle proprietà Opzioni di distribuzione e Server di distribuzione  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Esplora soluzioni **di**fare clic con il pulsante destro del mouse sul progetto, quindi selezionare **Proprietà**.  
  
2.  Nella finestra **Proprietà** fare clic su una proprietà, quindi digitare un valore o fare clic sulla freccia GIÙ per selezionare un'opzione di impostazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le proprietà di modellazione e alla distribuzione dei dati predefinite](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Proprietà del modello](../../analysis-services/tabular-models/model-properties-ssas-tabular.md)   
 [Distribuzione di una soluzione del modello tabulare](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
