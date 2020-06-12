---
title: Interfacce di query di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- predictions [Analysis Services], DMX prediction queries
- predictions [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- predictions [Analysis Services]
- queries [DMX], prediction queries
- mining models [Analysis Services], DMX
ms.assetid: a8952427-fd8c-4300-8f62-25f57ac1be0c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1702ad82c65b5a7370a62c4bc31a08007f374c9f
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84523159"
---
# <a name="data-mining-query-interfaces"></a>Interfacce di query di data mining
  Le query di data mining sono basate sul linguaggio DMX (Data Mining Extensions). È possibile utilizzare DMX per tutte le attività di stima e di modellazione, tra cui la classificazione, l'analisi dei rischi, la generazione di indicazioni e la regressione lineare. È inoltre possibile recuperare i modelli e le statistiche generate durante l'elaborazione del modello.  
  
 La sintassi per una query di stima nel linguaggio DMX è analoga a quella di una query eseguita in [!INCLUDE[tsql](../../includes/tsql-md.md)]. Sia in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] che in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] sono disponibili strumenti che consentono di compilare query di stima DMX.  
  
 In questo argomento vengono descritte le interfacce che possono essere utilizzate per creare ed eseguire query di data mining utilizzando DMX.  
  
 [Strumenti di query](#bkmk_Tools)  
  
-   [Generatore di query di stima](#bkmk_Builder)  
  
-   [Editor di query](#bkmk_QueryEditor)  
  
-   [Modelli DMX](#bkmk_Templates)  
  
-   [Integration Services](#bkmk_SSIS)  
  
 [Application Programming Interface](#bkmk_API)  
  
##  <a name="data-mining-query-tools"></a><a name="bkmk_Tools"></a>Strumenti query di data mining  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre gli strumenti seguenti per la compilazione di query di stima, query sul contenuto e query di definizione dei dati su oggetti di data mining:  
  
-   generatore delle query di stima  
  
-   Editor di query  
  
-   Modelli DMX  
  
-   Componenti di data mining di Integration Services  
  
###  <a name="prediction-query-builder"></a><a name="bkmk_Builder"></a> generatore delle query di stima  
 Il generatore delle query di stima è incluso nella scheda **Stima modello di data mining** di Progettazione modelli di data mining, disponibile in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando si utilizza il generatore delle query, è possibile utilizzare strumenti grafici per selezionare un modello di data mining e aggiungere nuovi dati del case e funzioni di stima. Il Generatore di query di stima include un editor di testo che è possibile utilizzare per modificare manualmente la query e un riquadro **risultati** semplice per visualizzare i risultati della query.  
  
###  <a name="query-editor"></a><a name="bkmk_QueryEditor"></a> Editor query  
 Nell'editor di query di sono [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] disponibili strumenti che è possibile utilizzare per compilare ed eseguire query DMX. È possibile connettersi a un'istanza di SQL Server Analysis Services e selezionare un database, le colonne della struttura di data mining e un modello di data mining. **Visualizzatore metadati** contiene un elenco di funzioni di stima che è possibile esplorare.  
  
###  <a name="dmx-templates"></a><a name="bkmk_Templates"></a>Modelli DMX  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] include modelli di query DMX interattivi che consentono di compilare query di questo tipo. Se l'elenco di modelli non è visualizzato, fare clic su **Visualizza** sulla barra degli strumenti e selezionare **Esplora modelli**. Per visualizzare tutti i modelli di Analysis Services, inclusi i modelli per DMX, MDX e XMLA, fare clic sull'icona del cubo.  
  
 Per compilare una query utilizzando un modello, è possibile trascinare il modello in una finestra Query aperta o fare doppio clic sul modello per aprire una nuova connessione e un nuovo riquadro query.  
  
 Per un esempio di come creare una query di stima da un modello, vedere [Creare una query di stima singleton da un modello](create-a-singleton-prediction-query-from-a-template.md).  
  
> [!WARNING]  
>  Nel componente aggiuntivo Data Mining per Microsoft Office Excel sono inoltre contenuti diversi modelli, insieme a un generatore delle query interattivo che può consentire la composizione di istruzioni DMX complesse. Per usare i modelli, fare clic su **Query**e su **Avanzate** nel client di data mining.  
  
###  <a name="integration-services-data-mining-components"></a><a name="bkmk_SSIS"></a>Integration Services componenti di data mining  
 È inoltre possibile includere query di stima come parte di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacchetto. Le attività e le trasformazioni seguenti in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] supportano la creazione ed esecuzione di query di stima DMX e istruzioni DMX.  
  
|Componente|Descrizione|  
|---------------|-----------------|  
|Attività Query di data mining|Consente di eseguire query DMX e altre istruzioni DMX come parte di un flusso di controllo.<br /><br /> In questo editor attività è presente il generatore delle query di stima e una casella di testo che consente di modificare la query DMX manualmente. Tuttavia, l'editor attività non può convalidare la query su oggetti in una soluzione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Pertanto, è consigliabile creare una query all'interno di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e incollare il testo dell'istruzione o eseguire una query nell'editor attività.|  
|Query di data mining - trasformazione|Consente di eseguire una query di stima in un flusso di dati utilizzando i dati forniti da un'origine del flusso di dati.<br /><br /> In questo editor attività è presente il generatore delle query di stima e una casella di testo che consente di modificare la query DMX manualmente.<br /><br /> La trasformazione può essere utilizzata solo per la creazione di query in cui vengono utilizzati dati nel flusso di dati; ovvero, query in cui viene utilizzata la sintassi PREDICTION JOIN. Questo componente non può essere utilizzato per l'esecuzione di query sul contenuto o di altri tipi di istruzioni DMX.|  
  
##  <a name="application-programming-interfaces"></a><a name="bkmk_API"></a>Interfacce di programmazione delle applicazioni  
 È possibile creare applicazioni personalizzate che consentono di eseguire query sui modelli di data mining utilizzando diversi linguaggi di programmazione, in combinazione con protocolli server quale OLE DB o un client ADOMD di Analysis Services. Per altre informazioni, vedere [Programmazione di data mining](../dev-guide/data-mining-programming.md).  
  
 Tuttavia, XMLA costituisce il formato di messaggio sottostante per tutte le interazioni con un server Analysis Services. All'interno di un messaggio XMLA, le query sono rappresentate in modo diverso a seconda se si invia una query di stima basata su DMX, una query sul contenuto o una query mediante la quale vengono recuperati i metadati del modello utilizzando i set di righe dello schema di data mining.  
  
-   Il testo delle **query di stima**, e tutte le altre istruzioni DMX, viene inviato in XMLA tramite il [metodo Execute &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute), con la query DMX posizionata come testo all'interno dell'[elemento Statement &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) dell'[elemento Command &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/command-element-xmla).  
  
-   Per recuperare il **contenuto del modello** e i **metadati del modello**, ad esempio il numero di cluster, gli attributi usati negli alberi delle decisioni, la data dell'ultima elaborazione del modello e i parametri dell'algoritmo usati durante la creazione del modello, è possibile usare il [metodo Discover &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) e specificare uno dei set di righe dello schema di data mining nell'intestazione dell'[elemento RequestType &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla). Per restringere l'ambito della query, immettere i criteri come restrizioni all'interno dell'elemento [RestrictionList Element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictionlist-element-xmla).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Soluzioni di data mining](data-mining-solutions.md)   
 [Informazioni sull'istruzione DMX SELECT](/sql/dmx/understanding-the-dmx-select-statement)   
 [Struttura e utilizzo di query di stima DMX](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)   
 [Creare una query di stima utilizzando la stima Generatore di query](create-a-prediction-query-using-the-prediction-query-builder.md)   
 [Creare una query DMX in SQL Server Management Studio](create-a-dmx-query-in-sql-server-management-studio.md)  
  
  
