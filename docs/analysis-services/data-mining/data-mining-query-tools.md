---
title: Strumenti Query di Data Mining | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 697a1c06a2d30d5721c122c557f3e41836335b02
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/08/2019
ms.locfileid: "65449948"
---
# <a name="data-mining-query-tools"></a>Strumenti query di data mining
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Tutte le query di data mining usano il linguaggio DMX (Data Mining Extensions). Il linguaggio DMX può essere usato per creare modelli per tutti i tipi di attività di apprendimento automatico, tra cui la classificazione, l'analisi dei rischi, la generazione di indicazioni e la regressione lineare. È anche possibile scrivere query DMX per recuperare informazioni sui modelli e le statistiche generati durante l'elaborazione del modello.  
  
 Si possono scrivere query DMX oppure è possibile compilare query DMX di base usando uno strumento come il **generatore delle query di stima** e quindi modificarle. Sia in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] che in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] sono disponibili strumenti che consentono di compilare query di stima DMX. Questo argomento descrive come creare ed eseguire query di data mining usando questi strumenti.  
  
-   [generatore delle query di stima](#bkmk_Builder)  
  
-   [Editor query](#bkmk_QueryEditor)  
  
-   [Modelli DMX](#bkmk_Templates)  
  
-   [Integration Services](#bkmk_SSIS)  
  
-   [Application Programming Interface](#bkmk_API)  
  
##  <a name="bkmk_Builder"></a> generatore delle query di stima  
 Il generatore delle query di stima è incluso nella scheda **Stima modello di data mining** di Progettazione modelli di data mining, disponibile in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando si usa il generatore delle query, è possibile selezionare un modello di data mining e aggiungere nuovi dati del case e aggiungere funzioni di stima. È quindi possibile passare a un editor di testo per modificare la query manualmente oppure al riquadro **Risultati** in cui vengono visualizzati i risultati della query.  
  
##  <a name="bkmk_QueryEditor"></a> Editor query  
 L'editor di query disponibile in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] consente anche di compilare ed eseguire query DMX. È possibile connettersi a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e selezionare un database, le colonne della struttura di data mining e un modello di data mining. **Visualizzatore metadati** contiene un elenco di funzioni di stima che è possibile esplorare.  
  
##  <a name="bkmk_Templates"></a> Modelli DMX  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] include modelli di query DMX interattivi che consentono di compilare query di questo tipo. Se l'elenco di modelli non è visualizzato, fare clic su **Visualizza** sulla barra degli strumenti e selezionare **Esplora modelli**. Per visualizzare tutti i modelli di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , inclusi i modelli per DMX, MDX e XMLA, fare clic sull'icona del cubo.  
  
 Per compilare una query utilizzando un modello, è possibile trascinare il modello in una finestra Query aperta o fare doppio clic sul modello per aprire una nuova connessione e un nuovo riquadro query.  
  
 Per un esempio di come creare una query di stima da un modello, vedere [Creare una query di stima singleton da un modello](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md).  
  
> [!WARNING]  
>  Nel componente aggiuntivo Data Mining per Microsoft Office Excel sono inoltre contenuti diversi modelli, insieme a un generatore delle query interattivo che può consentire la composizione di istruzioni DMX complesse. Per usare i modelli, fare clic su **Query**e su **Avanzate** nel client di data mining.  
  
##  <a name="bkmk_SSIS"></a> Componenti di data mining di Integration Services  
 È anche possibile includere le query di stima in un pacchetto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Le attività e le trasformazioni seguenti in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] supportano la creazione ed esecuzione di query di stima DMX e istruzioni DMX.  
  
|Componente|Descrizione|  
|---------------|-----------------|  
|Attività Query di data mining|Consente di eseguire query DMX e altre istruzioni DMX come parte di un flusso di controllo.<br /><br /> In questo editor attività è presente il generatore delle query di stima e una casella di testo che consente di modificare la query DMX manualmente. Tuttavia, l'editor attività non può convalidare la query su oggetti in una soluzione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Pertanto, è consigliabile creare una query all'interno di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e incollare il testo dell'istruzione o eseguire una query nell'editor attività.|  
|Query di data mining - trasformazione|Consente di eseguire una query di stima in un flusso di dati utilizzando i dati forniti da un'origine del flusso di dati.<br /><br /> In questo editor attività è presente il generatore delle query di stima e una casella di testo che consente di modificare la query DMX manualmente.<br /><br /> La trasformazione può essere utilizzata solo per la creazione di query in cui vengono utilizzati dati nel flusso di dati; ovvero, query in cui viene utilizzata la sintassi PREDICTION JOIN. Questo componente non può essere utilizzato per l'esecuzione di query sul contenuto o di altri tipi di istruzioni DMX.|  
  
##  <a name="bkmk_API"></a> Application Programming Interface  
 È possibile creare applicazioni personalizzate che consentono di eseguire query sui modelli di data mining utilizzando diversi linguaggi di programmazione, in combinazione con protocolli server quale OLE DB o un client ADOMD di Analysis Services. Per altre informazioni, vedere [Programmazione di data mining](../../analysis-services/data-mining/data-mining-programming.md).  
  
 Tuttavia, XMLA costituisce il formato di messaggio sottostante per tutte le interazioni con un server Analysis Services. All'interno di un messaggio XMLA, le query sono rappresentate in modo diverso a seconda se si invia una query di stima basata su DMX, una query sul contenuto o una query mediante la quale vengono recuperati i metadati del modello utilizzando i set di righe dello schema di data mining.  
  
-   Il testo delle **query di stima**, e tutte le altre istruzioni DMX, viene inviato in XMLA tramite il [metodo Execute &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute), con la query DMX posizionata come testo all'interno dell'[elemento Statement &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) dell'[elemento Command &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/command-element-xmla).  
  
-   Per recuperare il **contenuto del modello** e i **metadati del modello**, ad esempio il numero di cluster, gli attributi usati negli alberi delle decisioni, la data dell'ultima elaborazione del modello e i parametri dell'algoritmo usati durante la creazione del modello, è possibile usare il [metodo Discover &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) e specificare uno dei set di righe dello schema di data mining nell'intestazione dell'[elemento RequestType &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/requesttype-element-xmla). Per restringere l'ambito della query, immettere i criteri come restrizioni all'interno dell'elemento [RestrictionList Element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictionlist-element-xmla).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../../dmx/data-mining-extensions-dmx-reference.md)   
 [Soluzioni di data mining](../../analysis-services/data-mining/data-mining-solutions.md)   
 [Informazioni sull'istruzione DMX Select](../../dmx/understanding-the-dmx-select-statement.md)   
 [Struttura e utilizzo di query di stima DMX](../../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Creare una query di stima utilizzando Generatore query di stima](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)   
 [Creare una query DMX in SQL Server Management Studio](../../analysis-services/data-mining/create-a-dmx-query-in-sql-server-management-studio.md)  
  
  
