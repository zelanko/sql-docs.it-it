---
title: Drill-through sui modelli di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f179a467-7d03-4d61-8e9a-6b5afb5fc2d5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8cb5e932e2121efb9bd19375dfd2ff329c001812
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522523"
---
# <a name="drillthrough-on-mining-models"></a>Drill-through sui modelli di data mining
  Il termine*drill-through* fa riferimento alla possibilità di eseguire query su un modello o una struttura di data mining e di ottenere dati dettagliati non esposti nel modello.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dispone di due diverse opzioni per il drill-through dei dati del case. È possibile eseguire il drill-through nei case utilizzati per compilare i dati o nei case della struttura di data mining.  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>Drill-through nei case del modello e drill-through nella struttura  
 Il drill-through nei **case del modello** è utile per trovare dettagli aggiuntivi su regole, schemi o cluster in un modello. Ad esempio, non si utilizzeranno le informazioni di contatto del cliente per l'analisi in un modello di clustering, anche se i dati erano disponibili, utilizzando il drill-through, è possibile ottenere l'accesso a tali informazioni dal modello.  
  
 Al contrario, il **drill-through dei dati della struttura** consente l'accesso a informazioni non disponibili nel modello. Ad esempio, alcune colonne della struttura potrebbero essere state escluse da un modello perché il tipo di dati era incompatibile o i dati non erano utili per l'analisi.  
  
## <a name="enabling-drillthrough-on-a-model"></a>Abilitazione del drill-through in un modello  
 Per utilizzare il drill-through in un modello di data mining, è necessario soddisfare le condizioni seguenti:  
  
-   È possibile configurare il drill-through solo nei case del modello e non nella struttura di data mining, ma non viceversa.  In altre parole, è necessario abilitare il drill-through nel modello di data mining per consentire il drill-through nella struttura.  
  
-   Il drill-through sia nel modello sia nella struttura è disabilitato per impostazione predefinita. Se si utilizza Creazione guidata modello di data mining, l'opzione per abilitare il drill-through nei case del modello si trova nell'ultima pagina della procedura guidata.  
  
-   È possibile aggiungere la capacità di eseguire il drill-through in un modello di data mining esistente, ma in tal caso il modello deve essere rielaborato prima che sia possibile eseguire il drill-through nei dati.  
  
-   Il drill-through non funzionerà se non viene mantenuta la cache creata durante il processo di training. Per altre informazioni sulle proprietà di controllo della memorizzazione nella cache, vedere [Drill-through sulle strutture di data mining](drillthrough-on-mining-structures.md).  
  
## <a name="models-that-support-drillthrough"></a>Modelli che supportano il drill-through  
 Se un modello di data mining è stato configurato per consentire il drill-through e se si dispone delle autorizzazioni appropriate, quando si esplora il modello è possibile fare clic su un nodo nel visualizzatore adatto e recuperare informazioni dettagliate sui case in quel determinato nodo.  
  
 Non tutti i modelli supportano il drill-through; ciò dipende dall'algoritmo utilizzato per creare il modello. Nella tabella seguente vengono elencati i tipi di modelli che non supportano il drill-through o lo supportano con alcune limitazioni. Se il tipo di modello non è elencato, significa che supporta il drill-through.  
  
|**Nome algoritmo**|**Supporto del drill-through**|  
|------------------------|----------------------------------|  
|Algoritmo Microsoft Naive Bayes|Non supportata.<br /><br /> Questi algoritmi non assegnano case ai nodi specifici nel contenuto.|  
|Algoritmo Microsoft Neural Network|Non supportata.<br /><br /> Questi algoritmi non assegnano case ai nodi specifici nel contenuto.|  
|Algoritmo Microsoft Logistic Regression|Non supportata.<br /><br /> Questi algoritmi non assegnano case ai nodi specifici nel contenuto.|  
|Algoritmo Microsoft Linear Regression|Supportata.<br /><br /> Tuttavia, poiché il modello crea un solo nodo, `All`, il drill-through restituisce tutti i case di training del modello. Se le dimensioni del set di training sono elevate, il caricamento dei risultati può richiedere molto tempo.|  
|Algoritmo Microsoft Time Series|Supportata.<br /><br /> Non è tuttavia possibile eseguire il drill-through ai dati della struttura o del case usando il **Visualizzatore modello di data mining** in Progettazione modelli di data mining. È necessario creare invece una query DMX.<br /><br /> Inoltre, non è possibile eseguire il drill-through su nodi specifici o scrivere una query DMX per recuperare case in nodi specifici di un modello Time Series. È possibile recuperare dati del case dal modello o dalla struttura utilizzando altri criteri, ad esempio una data o i valori dell'attributo.<br /><br /> Se si desidera visualizzare i dettagli dei nodi ARTXP e ARIMA creati dall'algoritmo Microsoft Time Series, può essere più semplice usare [Microsoft Generic Content Tree Viewer &#40;Data mining&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).|  
  
## <a name="related-tasks"></a>Attività correlate  
 Per ulteriori informazioni su come utilizzare il drill-through con i modelli di data mining, vedere gli argomenti seguenti:  
  
|Attività|Collegamenti|  
|-----------|-----------|  
|Utilizzare il drill-through nei visualizzatori dei modelli di data mining|[Utilizzare il drill-through dai visualizzatori modello](use-drillthrough-from-the-model-viewers.md)|  
|Recuperare dati del case per un modello tramite il drill-through|[Eseguire il drill-through sui dati del case da un modello di data mining](drill-through-to-case-data-from-a-mining-model.md)|  
|Abilitare il drill-through su un modello di data mining esistente|[Abilitare il drill-through per un modello di data mining](enable-drillthrough-for-a-mining-model.md)|  
|Per tipi di modelli specifici, vedere gli esempi di query drill-through.|[Query di data mining](data-mining-queries.md)|  
|Abilitare il drill-through in Creazione guidata modello di data mining|[Completamento procedura guidata &#40;Creazione guidata modello di data mining&#41;](../completing-the-wizard-data-mining-wizard.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Drill-through sulle strutture di data mining](drillthrough-on-mining-structures.md)  
  
  
